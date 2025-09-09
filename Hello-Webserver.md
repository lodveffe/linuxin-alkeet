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

  ## Tehdään uusi name-based virtual host

  Tässä vaiheessa täytyy palauttaa muistia vierailemalla [Johannan repolla](https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-03092025.md).

  Okei eli ensiksi tehdään konffitiedosto. Siirryn sites-available hakemistoon.

          cd /etc/apache2/sites-available

  Sitten se konffitiedosto nimeltä hattu.conf

          sudo micro hattu.conf

  Itse asiassa taidan kopsata site1.com.conf tiedoston ja nimetä sen hattu.conf ja muokata sitä niin pääsen vähän helpommalla.

          sudo cp site1.com.conf hattu.conf

  No nyt kun on muokattu konffitiedostot, niin pistetääs uusi sivusto käyttöön ja vanha poies.

          sudo a2dissite site1.com.conf
          sudo a2ensite hattu.conf
          sudo systemctl reload apache2

  Ja testataas `curl hattu.com`

  Hetken olin hämilläni että oonko hakkeroinut jonkun vai mikä homma kun tuli kaikenmaailman infoa eri hatuista ja yhteystietoja esiin, kunnes tajusin että sivuston nimihän on `hattu.example.com`... Testataas sillä.

  could not resolve host.... hmmm

  No niinhän se oli että täytyi lisätä /etc/hosts-tiedostoon rivi `hattu.example.com`

  <img width="882" height="256" alt="image" src="https://github.com/user-attachments/assets/9956c378-f5cd-47e6-8486-06192be445ad" />

  Okeei nyt se kyllä latasi sivun, mutta sen defaultin eikä hatun oman html... let's see mikä meni mönkään

  <img width="882" height="256" alt="image" src="https://github.com/user-attachments/assets/cc459339-9eff-41d3-a012-345a04a6de3b" />

  Ei ihme että meni mönkään. Olin unohtanut pisteet hattu.example.comista... Tässä huomaa kuinka pienestä voi olla kiinni. Korjataas ne ja testataan uudestaan.

  <img width="873" height="119" alt="image" src="https://github.com/user-attachments/assets/273f368f-b392-45c3-a681-1dcb76781404" />

  No nyt!

  ## Validi HTML5-sivu

  Tehdään sivustosta hieman siistimpi lisäämällä HTML-koodia, eli headereita bodya yms.

  Huomasin, että index.html, vaikka onkin kotihakemistossani, niin on rootin omistama tiedosto, eli tarvitsin sudoa sitä muokatakseni. Näin vaihdoin tiedoston omistajan:

  <img width="871" height="179" alt="image" src="https://github.com/user-attachments/assets/57c4682a-8087-48d7-90f0-1e9525c9ed38" />

  Nyt pystyn ilman sudoa muokkaamaan sivustoa.

  Lopputulos:

  <img width="1104" height="465" alt="image" src="https://github.com/user-attachments/assets/4b102aeb-0a32-4b02-9688-d77fe4a0178b" />

  Ois varmaan pitänyt ottaa niitä CSS-kursseja...

  `curl` näyttää koko sivuston:

  <img width="914" height="328" alt="image" src="https://github.com/user-attachments/assets/d541ca70-7d76-4a3b-924e-aca577e3eca1" />

  kun taas `curl -I` näyttää sivuston headerin. Tässä screenshotti curlin manual pagesta:

  <img width="1213" height="261" alt="image" src="https://github.com/user-attachments/assets/66e1ec2a-8aca-470a-9e71-df6dfed08367" />

  Eli `curl -I` tai `(--head)` tekee pelkästään header-pyynnön palvelimelle, eikä hae sivun koko sisältöä, vain otsakkeet.

  Tässä tuloste `curl -I hattu.example.com` 

  <img width="729" height="209" alt="image" src="https://github.com/user-attachments/assets/ebc725ca-903d-44f5-9776-71793fc4005b" />

  Siinä näkyy tiiviimmässä paketissa infoa sivustosta. E-tag on tunniste, jolla selain ja palvelin pysyvät kärryillä siitä, onko sivua muokattu. Jos ei ole ja e-tag on sama kuin viime kerralla kun sivustolla on vierailtu, niin selain voi ladata käyttäjälle sivuston nopeammin välimuistista. [Tästä siitä lisää](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/ETag)

  Huhhuh oli taas paljon asiaa. Seuraavalla tunnilla saankin tämän hienon hattusivuston koko internetille auki pilvipalvelimen avulla.
