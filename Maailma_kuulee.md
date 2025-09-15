# Maailma kuulee!

Viikon tehtävänä oli vuokrata pilvestä palvelin ja asentaa sille weppipalvelin.
No sehän tuli jo luennolla tehtyä, kun toimin Teron mannekiininä, joten ajattelin nyt sitten tehdä tuon vapaaehtoisen tehtävän, eli laittaa tuohon julkiseen palvelimeen uusi name based virtual host.

Täytyy ottaa taas [Johannan repo](https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-03092025.md) tähän lunttilapuksi.

Eli ekaks tehdään uudelle sivulle conffifile

    sudo micro /etc/apache



<img width="906" height="535" alt="image" src="https://github.com/user-attachments/assets/e6bbccbd-31dc-4849-841a-7a37243d5667" />




    sudo apache2ctl configtest

<img width="861" height="106" alt="image" src="https://github.com/user-attachments/assets/f969f174-ebfc-418f-bfaa-c7d98416c0b0" />


No sieltähän saatiin suora vastaus. Eli kirjotusvirhe!


<img width="876" height="349" alt="image" src="https://github.com/user-attachments/assets/eb33f307-ce24-4568-94d8-ea813b3d9617" />


<img width="866" height="164" alt="image" src="https://github.com/user-attachments/assets/05db2be0-bb5b-48a6-aa80-50ae052fe670" />
Eikö mulla ole sitten asetettu oikeuksia oikein?

<img width="861" height="250" alt="image" src="https://github.com/user-attachments/assets/9e1d8ab1-ec75-47cf-9ae3-fa69cc53fa79" />

emt kaikkea tässä on nyt testattu mutta silti:

<img width="830" height="218" alt="image" src="https://github.com/user-attachments/assets/e1c85749-1cc1-4596-8590-cb5f853cbcdc" />

Nyt en jaksa enään kikkailla tän kaa. antaa olla. joku viis tuntia tässä koitin troubleshoottaa.

Okei saavuin takas skidi huilimisen jälkeen. testaillaas taas...

Lisäsin uussivu.com.conffiin Directory-lohkoon tämmöset setit
<img width="841" height="262" alt="Screenshot from 2025-09-15 22-27-07" src="https://github.com/user-attachments/assets/473bb0b0-01bd-4768-9de8-a8208204d27c" />

Hallelujaah vihdoin skulaa, mutta mikä ihmeen index??


<img width="830" height="218" alt="image" src="https://github.com/user-attachments/assets/29304e89-f7b1-4f14-9384-0440beb8f462" />

Täytyy myöntää että nyt kyllä tässä vaiheessa käyn jo kiivasta keskustelua ChatGPT:n kanssa. Selvisi semmoinen, ettei mitään tätä 403 error-rumbaa olisi ollut, jos olisin tehnyt muutoksia index.html nimiseen tiedostoon, mutta kun sen sijaan käytän uussivu.html-nimistä, niin apache ei tiennyt mitä näyttää. Mutta kun lisättiin nuo aikaisemmat Directorylohkoon Options Indexes, niin apache osaa näyttää jotain muuta kuin sen index.html

        mv /home/marek/public-sites/uussivu.html index.html


<img width="841" height="262" alt="image" src="https://github.com/user-attachments/assets/9d7a8202-dd4e-4b36-9af6-e7f12d10d4bb" />

Huhhuh meni tässäkin joku 7h sit yhteensä...
