# Hello Webserver

- On olemassa kaksi päätyyppiä palvelinten toimintaan: IP-based virtual hosting ja name-based virtual hosting
    IP-hostingissa jokaiselle palvelimelle täytyy olla oma IP-osoite, kun taas jälkimmäisessä yhdellä IP-osoitteella voi olla monta palvelinta.
    Name-based kuitenkin ensimmäiseksi tsekkaa ip-osoitteen, eikä vielä katso domain-nimeä. Jos monta eri virtualhostia voi vastata pyyntöön, niin silloin vasta kurkataan ServerName ja ServerAlias lohkojen arvoihin ja verrataan niitä domain-nimeen ja valitaan parhaiten sopiva matchi.
  
    lähde: The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation: [Name-based Virtual Host Support](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)

  ## Testeihin

  Katsotaan, vastaako weppisivu localhost-osoitteesta. Ensiksi katson onko Apache jotenkin maagisesti käynnistynyt automaattisesti:

      sudo systemctl is-active apache2

  Sanoo että active on. Selvä. Eli kaiken järjen mukaan kun curlaa localhostin niin pitäisi kaiken olla ok.

      curl localhost

  Ja sieltähän sitä koodia tuli terminaalille.

  Entäpä tästä curlauksesta syntyneet lokit? Kurkataas sinne.

      tail -f /var/log/apache2/access.log #tuo -f meinaa follow, eli päivittää lokit tulostettuina sitä mukaa, kun sinne niitä syntyy

  Tuli että access denied. Niinhän se oli että tuo on järjestelmän lokitiedosto, eikä sinne pääse ilman sudoa. Testataas uudestaan sudon kanssa.

  <img width="856" height="91" alt="image" src="https://github.com/user-attachments/assets/9f8b7873-9c0a-42c1-b507-dcf7ea0773b7" />

  Ja siitähän sitä suoraan näkee, kuinka viimeisin curl on päässyt perille onnistuneesti. Avataan tämä rivi selkokielelle:

  Ekaksi näkyy mistä pyyntö tuli, eli tässä se oli localhost `127.0.0.1`, mutta ilmoitettu ip6-versiona eli `::1`

  Seuraavaa kohtaa täytyi googlailla eli tuota `- -`, ja se näyttäisi liittyvän HTTP Authenticationiin. Eli jos sivu olisi käyttäjätunnuksen ja salasanan takana ja siellä vierailtaisiin, niin tuossa `- -`-kohdassa näkyisi tunnarit. Näitä konffeja saa asetettua Apachen ohjelman `htpassword` avulla.

  Tähän väliin aikaleima.

  `GET / HTTP/1.1` -> kun käytettiin `curl` niin se lähetti HTTP GET-pyynnön palvelimelle, pyytäen pääsyä resurssiin, eli tässä tapauksessa weppisivuun. `/` GETin jälkeen tarkoittaa resurssin polkua palvelimella,      eli missä se etusivu sijaitsee; DocumentRootissa

  <img width="882" height="256" alt="image" src="https://github.com/user-attachments/assets/6a623c57-70ab-48ea-a56c-3c23bd7e31fb" />

  Täältä näkyy, mihin `GET /` johtaa – /var/www/html
  Jos oltaisiin curlattu jotain muuta kuin etusivua, niin lokissa olisi näkynyt sen resurssin sijainti `/`jälkeen esim `GET /laksut.html`

  HTTP1.1 puolestaan meinaa protokollaa, joka määrittelee säännöt, miten selain ja palvelin kommunikoivat.

  `200` meinaa että kaikki OK. HTTP-statuskoodi

  `10705` on tavujen määrä, jota siirrettiin

  tuo `"-"` on referer, joka kertoo, mistä clientti koittaa saapua sivulle. Jos käyttäjä hakee sivun suoraan osoiteriviltä, niin se jää tyhjäksi, niinkuin nyt. Muuten siinä näkyisin sen sivun URL, josta käyttäjä  saapui esim. linkin kautta.

  viimeisimpänä lokissa näkyy `"curl/8.14.1"`. Tämä on user-agent, joka kertoo palvelimelle, mikä ohjelma teki pyynnön. Jos olisi esim. Mozillalla hakenut localhostia, niin tässä näkyisi `"Mozilla/5.0"`

  
  
