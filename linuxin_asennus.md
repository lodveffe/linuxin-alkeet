# Ykkösotsikko
Linuxin läksyjen raportit

## h1 - Linuxin lataaminen virtuaalikoneelle
Koitin ladata läppärilleni, (HP envy x360 convertible 15-dr0002no), jossa on Ubuntu 24.04 käyttiksenä, VirtualBoxin kautta debian 13.live-virtuaalikonetta [Johannan ohjeiden mukaan](https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-20082025.md) ja erroria ilmestyi:
<img width="600" height="354" alt="Screenshot from 2025-08-25 14-33-02" src="https://github.com/user-attachments/assets/bca3367e-bdf9-4a44-a338-2267d6b251f2" />
<img width="206" height="289" alt="Screenshot from 2025-08-25 14-33-42" src="https://github.com/user-attachments/assets/2aa58f06-c16c-4b47-a0e2-3e46d8a80b97" />

Tämä sama errori oli tullut aikaisemmin, kun koitin ladata toista linux-distroa. Kovasti koitin muunnella kaikenmaailman asetuksia, mutta ei mikään auttanut. Päivitin kaikki ajurit, toivoen että ongelma lähtisi sillä, mutta ei. Sitten tulikin seuraavanlainen ongelma:

![20250818_180944](https://github.com/user-attachments/assets/1815eb8f-38be-4748-884a-8b3c576c4112)

Näyttäisi siltä että jokin komponentti oli mäsänä läppärissä. Vituttihan se, mutta ajattelin, että no ainakin ratkesi syy sille, miksi tuli aikaisemmin erroria virtuaalikoneen kanssa.
Kävin ostamassa torista uuden läppärin (ThinkPad t14 gen 2, intel-versio),latasin sille myös dual-boottina Ubuntun, ja kuinkas ollakaan sillä tuli samat errorit.
Googlailemalla huomasin kyllä, että monilla Ubuntun käyttäjillä oli samanlaisia kriittisiä erroreita VirtualBoxin kanssa. Joku nettifoorumilla neuvoi palauttamaan VirtualBoxin aikaisempaan versioon, mutta jo kymmenen tuntia kamppailleena luovutin VirtualBoxin suhteen ja tein kuten Lari Iso-Anttila neuvoi, eli karttamaan VirtualBoxin kaukaa ja lataamaan esimerkiksi VMware workstationin, joka on nyt saatavilla yksityiskäyttöön ilmaiseksi. Teinkin juuri niin ja nyt pelittää ongelmitta. 

Jatkossa raportit tulevat varmasti olemaan kattavampia ja tulen syventymään yksityiskohtaisemmin ongelmanratkaisuihin ja tiedonhakuun. Nyt oli vaan kiire saada toimiva laite käsiini.

