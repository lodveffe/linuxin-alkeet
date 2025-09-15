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


<img width="861" height="250" alt="image" src="https://github.com/user-attachments/assets/9e1d8ab1-ec75-47cf-9ae3-fa69cc53fa79" />

emt kaikkea tässä on nyt testattu mutta silti:

<img width="830" height="218" alt="image" src="https://github.com/user-attachments/assets/e1c85749-1cc1-4596-8590-cb5f853cbcdc" />

Nyt en jaksa enään kikkailla tän kaa. antaa olla. joku viis tuntia tässä koitin troubleshoottaa.

