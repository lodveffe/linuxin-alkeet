# Nimen vuokraaminen

Eli tämän viikon tehtävänä oli vuokrata domain-nimi netistä ja pistää se osoittamaan julkiseen weppipalvelimeen. Eiköhän aloiteta itse nimen vuokraamisesta.

Päätin mennä nyt NameCheapilla, vaikka olisi saanut GitHub Educationin kautta ilmaiseksi. Käydääs tsekkaamassa NameCheapilta mitä tarjouksia tulee hakusanalla `lofving`

<img width="1276" height="929" alt="image" src="https://github.com/user-attachments/assets/5f784c39-87d6-4d7c-8b9b-a5f0502085cd" />

Toi `lofving.it.com` ois aika hauska, mutta en tiiä kuulostaako se liikaa mäkkärin `i'm lovin' it`- motolta. `lofving.inc` taas vähän yli budjetin... Täytynee hakea eri nimellä.

<img width="1286" height="315" alt="image" src="https://github.com/user-attachments/assets/fb20b342-ff14-430d-b710-ce77974b7032" />

Taidan sittenkin käydä katsomassa miten se Education paketti toimii. brb
Linkitin äsken pöytäkoneella tuon GitHub Educationin Namecheappiin, ja sain voudeksi ilmaisen lofving.me-nimen. Prosessi oli erittäin simppeli. Piti vain linkittää GitHub käyttäjä Namecheappiin ja valita nimi. Jakavat ilmaiseksi .me -päätteillä olevia nimiä. Jossain vaiheessa kassalla luki kyllä että antavat niitä vain Australiaan ja johonkin muualle, mutta läpi näytti menevän, niinkuin alhaalla olevasta screenshotista näkyy.

<img width="1081" height="583" alt="14063bcad50401318e8a6cac0dcabb13" src="https://github.com/user-attachments/assets/bd05cf25-1948-49f3-b6a6-613073a3f583" />

Tässä vaiheessa muistin, että UpCloud, jolta olin vuokrannut palvelimen pilvestä, oli poistanut sen serverin käytöstä ilmaisen kokeilujakson päätyttyä.
UpCloud on näköjään myös samalla poistanut käyttäjäni tai vähintään shadowbännännyt mut, sillä en pääse kirjautumaan enään sisään, enkä pysty resetoida salasanaa. Tästähän on ollut puhetta tunneilla että sivustot ja yritykset helposti pistää välit poikki jos on vähänkään 'epäilyttävää' käytöstä. Eli varmaan kun olin syöttänyt niille luottokorttitietojen sijaan kertakäyttöisen debitkortin ja ottanut vaan viikon ilmaista aikaa, niin eivät tykänneet hyvää...

![maxresdefault](https://github.com/user-attachments/assets/5c2375dc-aac0-4bbc-b0ad-d0d0546c0ae6)

Jooh olinkin vaan koittanut päästä väärillä tunnareilla sisään. Mutta serveri oli kuitenkin poissa, niin täytyi lisätä UpCloud-tilille massia ja pistää uusi tulemaan:

<img width="871" height="318" alt="ecb644ed1253d6c86cc4330b2c37eaf4" src="https://github.com/user-attachments/assets/91efc21a-652e-45d0-8f69-ee7797ab991f" />

Taidan palauttaa tämän raportin jo etuajassa, kun täytyy alkaa tuon serverin kanssa taas temmeltämään... Lisään myöhemmin tänne loput tehtävät!

## Uusi yritys

No nyt on uusi palvelin pyörimässä ja alkuasetukset tehty, eli luotu oma käyttäjä, poistettu root-tili käytöstä, asennettu apache ja tulimuuri päällä reikien kera. Hyvää harjoitusta.

`lofving.me` osoittaa nyt weppipalvelimeeni. 

<img width="595" height="129" alt="image" src="https://github.com/user-attachments/assets/3b5f3ff6-46c8-4c10-8d26-97e6cbbb06fc" />

Täytyi vain muokata A-record namecheapin domain-asetuksista osoittamaan UpCloud-ip-osoitteeseen,

<img width="1157" height="663" alt="image" src="https://github.com/user-attachments/assets/4c0411f4-4b85-4cc3-b8b8-e8ef975997a6" />

ja muokata Apachen VitrualHost conffia lisäämällä dns-nimi ServerName ja ServerAlias kohtiin:

`sudo micro /etc/apache2/sites-available/lofving.me.conf`

<img width="640" height="337" alt="image" src="https://github.com/user-attachments/assets/c52c5feb-7ab8-4218-9867-a4313473a331" />

ja toki `sudo a2ensite lofving.me.conf`
        `sudo systemctl reload apache2`

## Alidomainien lisääminen

onnistuu helposti lisäämällä uuden recordin NameCheapin DNS-asetuksiin,

<img width="1166" height="353" alt="image" src="https://github.com/user-attachments/assets/e3f2dfd4-9eec-4517-85fc-a591252584fb" />

ja lisäämällä myös uuden VirtualHostin:

<img width="691" height="431" alt="image" src="https://github.com/user-attachments/assets/5fe5e171-a667-4bd6-bbab-cffc1810a310" />

`sudo systemctl reload apache2`

<img width="691" height="431" alt="image" src="https://github.com/user-attachments/assets/86019615-0b0c-4b7a-82fc-83c34e8e8140" />

Okei, jostain syystä tuli tämä klassinen errori. Lähdetääs tutkimaan asiaa.

<img width="815" height="156" alt="image" src="https://github.com/user-attachments/assets/4dec2dfc-c3e1-471d-a0af-3e63da1b9990" />


Testasin luoda uuden VirtualHost-conf-tiedoston alidomainille, jolla on myös oma documentroot, ja sehän sitten toimikin!

<img width="815" height="156" alt="image" src="https://github.com/user-attachments/assets/5d9e292c-f050-4e09-be3b-73e7bd8d485d" />

eli `sudo cp /etc/apache2/sites-available/lofving.me.conf /etc/apache2/sites-available/linuxkurssi.lofving.me.conf`,
sieltä muutin vain servernamen `linuxkurssi.lofving.me` ja documentrootin `/home/marek/lofving/alidomain/linuxkurssi`

## host ja dig -komennot

Tutkitaan näiden komentojen avulla muutamien sivujen DNS-tietoja.

<img width="804" height="245" alt="image" src="https://github.com/user-attachments/assets/9b80c1b1-71f5-4afb-bf62-85bfbc2746d1" />

<img width="806" height="486" alt="image" src="https://github.com/user-attachments/assets/1c3fa639-90b5-4637-8220-f49d17e66450" />

## Lähteet

UpCloud. 2025. https://upcloud.com/

GitHub Education. 2025. https://github.com/education

NameCheap. 2025. https://www.namecheap.com/

Tero Karvinen. 2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/

Tero Karvinen. 2025. linux-palvelimet. https://terokarvinen.com/linux-palvelimet/

