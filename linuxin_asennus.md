# Ykkösotsikko
Linuxin läksyjen raportit

## h1 - Linuxin lataaminen virtuaalikoneelle
Koitin ladata läppärilleni, (HP envy x360 convertible 15-dr0002no), jossa on Ubuntu 24.04 käyttiksenä, VirtualBoxin kautta debian 13.live-virtuaalikonetta [Johannan ohjeiden mukaan](https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-20082025.md) ja erroria ilmestyi:
<img width="600" height="354" alt="Screenshot from 2025-08-25 14-33-02" src="https://github.com/user-attachments/assets/bca3367e-bdf9-4a44-a338-2267d6b251f2" />
<img width="206" height="289" alt="Screenshot from 2025-08-25 14-33-42" src="https://github.com/user-attachments/assets/2aa58f06-c16c-4b47-a0e2-3e46d8a80b97" />

Tämä sama errori oli tullut aikaisemmin, kun koitin ladata toista linux-distroa. Kovasti koitin muunnella kaikenmaailman asetuksia, mutta ei mikään auttanut. Päivitin kaikki ajurit, toivoen että ongelma lähtisi sillä, mutta ei. Sitten tulikin seuraavanlainen ongelma:

![20250818_180944](https://github.com/user-attachments/assets/1815eb8f-38be-4748-884a-8b3c576c4112)

Näyttäisi siltä että jokin komponentti oli mäsänä läppärissä. V*tuttihan se, mutta ajattelin, että no ainakin ratkesi syy sille, miksi tuli aikaisemmin erroria virtuaalikoneen kanssa.

Kävin ostamassa torista uuden läppärin (ThinkPad t14 gen 2, intel-versio), latasin sille myös dual-boottina Ubuntun, ja kuinkas ollakaan sillä tuli samat errorit.
Googlailemalla huomasin kyllä, että monilla Ubuntun käyttäjillä oli [samanlaisia kriittisiä erroreita VirtualBoxin kanssa](https://askubuntu.com/questions/1521259/virtualbox-error-message-a-critical-error-has-occurred-while-running-the-virtua).
Joku nettifoorumilla neuvoi palauttamaan VirtualBoxin aikaisempaan versioon, mutta jo kymmenen tuntia kamppailleena luovutin VirtualBoxin suhteen ja tein kuten Lari Iso-Anttila neuvoi, eli karttamaan VirtualBoxin kaukaa ja lataamaan esimerkiksi VMware workstationin, joka on nyt saatavilla yksityiskäyttöön ilmaiseksi. Teinkin juuri niin ja nyt pelittää ongelmitta. 

Jatkossa raportit tulevat varmasti olemaan kattavampia ja tulen syventymään yksityiskohtaisemmin ongelmanratkaisuihin ja tiedonhakuun. Nyt oli vaan kiire saada toimiva laite käsiini.

__PÄIVITYS__

Tulin päivittämään raporttia ja lisäämään vaiheet virtuaalikoneen lataamiseen VMWarella.

<img width="918" height="738" alt="image" src="https://github.com/user-attachments/assets/27414ccf-a81d-4e2d-b966-85aceca683e2" />

Valitsin tuon suositellun asennuksen. Myöhemmin pääsee kuitenkin muuttamaan RAMia ja säkeitä.

<img width="918" height="738" alt="image" src="https://github.com/user-attachments/assets/c8115463-dca9-4f4e-98fa-8f3797549bdb" />

Valitsin lataustyypiksi ISO-imagen, joka on Debian 13. Latasin sen [täältä](https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/) 

<img width="918" height="738" alt="image" src="https://github.com/user-attachments/assets/82d717b9-3e60-4747-bb27-65f02625a0ed" />

Koska VMWare ei tunnistanut käyttöjärjestelmää eikä luettelosta löytynyt Debian 13, niin valitsin Other Linux 6.X kernel 64-bit

Seuraavaksi valitaan levytilan määrä ja että onko levy yhtenä tiedostona vai jaotettuna moneen. Multiple filessa eduksi VMWare kertoo olevan se, että tiedostoja on helpompi siirrellä tietokoneiden välilä. Valitsin single-file, sillä en ole siirtämässä mitään kyseisellä virtuaalimasiinalla. Muistia kannattaa myös varata enemmän kuin tuon oletus 8gb. Mutta menin sillä.

<img width="918" height="738" alt="Screenshot from 2025-10-07 16-20-06" src="https://github.com/user-attachments/assets/effee25b-0881-4cfe-9609-45e0d3d49e1d" />

Tässä saa vielä muutella virtuaalikoneen rautaa. Laitan lisää RAMia, jotta kaikki pelittää sulavasti. Muuhun en koske.

<img width="918" height="738" alt="image" src="https://github.com/user-attachments/assets/209cd318-982c-468e-a9d2-63a23c9a63aa" />

Ja näin sutjakkaasti päästinkin jo Boot menuun!

<img width="645" height="483" alt="image" src="https://github.com/user-attachments/assets/90d809f3-0f1f-44c9-b6b5-e6729351fd16" />

Live-tilassa voi mennä ja kokeilla wörkkiikö kaikki toivotusti, ja päättää haluaako jatkaa asentamaan itse käyttöjärjestelmän. Tässä tilassa mikään ei pysyvästi tallennu.
Alempana on vaihtoehto suoraan asentaa Debian. Päätän mennä live-tilalla, kun näitä virtuaalikoneita löytyy jo.

<img width="1284" height="808" alt="image" src="https://github.com/user-attachments/assets/9a225356-7685-4c9d-81b8-cdd11a879170" />

Sisälle päästiin. Työpöydältä löytyi myös installeri, jos päättää asentaa käyttiksen. Se 8GB ei taida riittää siihen.

<img width="1284" height="808" alt="image" src="https://github.com/user-attachments/assets/e481375a-dfce-4d8a-ab09-73c052f71b31" />

Eikä riittänytkään. No mutta ei se mitään, kun löytyy jo toinen Debian 13 virtuaalikone.

## Lähteet

Debian. (n.d). Haettu 7.10.2025. https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/

Johanna, H. (2025). linux-20082025.md [Source Code]. https://github.com/johannaheinonen/johanna-test-repo/

Tero Karvinen. 2025. linux-palvelimet. https://terokarvinen.com/linux-palvelimet/

Ask Ubuntu. 2024. Virtualbox error message a critical error has occurred while running the virtual machine https://askubuntu.com/questions/1521259/virtualbox-error-message-a-critical-error-has-occurred-while-running-the-virtua
