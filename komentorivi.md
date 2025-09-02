# Komentorivin perusteet

## Peruskomentoja:

[Laitan Teron komentorivicheatsheetin tänne](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)

Ladataanpas muutamat komentoriviohjelmat.
Kaikki löyty kun Googlaili käyttäjien lemppari komentorivityökaluja.

Tekstinmuokkausohjelma:

    sudo apt install micro

Jonkin sortin lyhennetty versio manual pageista, kun ei jaksa lukea kaikkea läpi

    sudo apt install tldr

Paranneltu versio cat-ohjelmasta:

    sudo apt install bat

Prosessien tarkkailutyökalu. Päivitetty versio top-ohjelmasta

    sudo apt install htop

Testataanpas ladata nämä kaikki yhdellä komennolla

    sudo apt install tldr bat htop 

Näköjään se löysi vain tldr noista ja htop taisi olla jo ladattuna. Katotaas mitä se sanoo jos kirjoittaa vaan bat

<img width="570" height="187" alt="image" src="https://github.com/user-attachments/assets/fc429cab-9a97-402b-96d4-4feb5ba06eab" />

Okeei no ei se kyllä toi paketti ole. Varmistin sen vielä menemällä nettisivulle jossa kerrotaan infoa batista. 
<img width="700" height="359" alt="image" src="https://github.com/user-attachments/assets/8da9db99-3b3a-4687-9be8-582b439bb432" />

Mutta sitten testasin

    sudo apt install bat

ja näin se sanoi?
<img width="696" height="269" alt="image" src="https://github.com/user-attachments/assets/37102460-1222-4d45-8cd8-843c9873bb1a" />

Hämmentävää. Ehkä se sitten latasi kaiken aikaisemmalla komennolla.

## Tärkeät kansiot

Kun halutaan roottiin, eli kaiken juurelle, niin

        cd /

tai sitten vaan tsekataan että missä mennään komennolla ls ja siirrytään ylöspäin kansioissa kohti roottia cd ..
<img width="861" height="395" alt="image" src="https://github.com/user-attachments/assets/55d01d8a-6f47-4ecd-a28e-7650b2833861" />

roottikansio sisältää siis kaiken. Mukaan lukien käyttäjien kotikansiot, joihin pääsee takaisin 

        cd home/käyttäjä/
        tai sitten cd ~
        #tuosta kiekurasta tietää että on kotikansiossa^
        
mutta takaisin ihmettelemään rootkansiota.

etc/-kansiota tutkiessani löysin papersize-nimisen tiedoston. Kurkataanpa sinne.
<img width="803" height="170" alt="image" src="https://github.com/user-attachments/assets/ce35c263-c332-4786-a070-239dc314cadd" />

Eli etc/ on täynnä siis tekstipohjaisia asetustiedostoja.

/media/ sisältää automaattisesti liitetyt usb-tikut, cd-levyt, ulkoiset kovalevyt, ISO-tiedostot yms. 

<img width="800" height="284" alt="image" src="https://github.com/user-attachments/assets/94159d28-1b72-40ec-93e6-4b4f14aaa370" />

Tuosta näkyy kuinka ekaksi media/loffe/ ei sisältänyt mitään, kunnes tokan `ls`-komennon kohdalla olin liittänyt Ubuntun sisältävän USB-tikun.

Kurkataas sitten myös /var/log/syslog. Testataan lukea sitä käyttämällä absoluuttista polkua.

        cat /var/log/syslog
        
<img width="810" height="416" alt="image" src="https://github.com/user-attachments/assets/3dc55be8-fee4-477e-8f7d-18355e082c46" />

no huhhuh en kyllä ihan niin pitkällä opintoja ole, että tosta ymmärtäisin.

        batcat /var/log/syslog
        
<img width="810" height="416" alt="image" src="https://github.com/user-attachments/assets/669bb478-2d25-4fdd-a3a6-a9526d8d9dbf" />

Vähän lisäsi tuo bat väriä tulosteeseen, mutta ei mun ymmärrykseen. Toivottavasti tämän kurssin jälkeen saa tuosta jotain tolkkua :)

Tutustutaan vielä `grep`-komentoon. Samalla voidaan verrata tuota `tldr`-työkalua, jonka latasin, manual pagesiin eli `man`

        man grep

<img width="808" height="528" alt="image" src="https://github.com/user-attachments/assets/6431a536-d887-4acb-93d6-f7b3b1fe4a27" />

647 riviä manuaalia, joka ohjaa lopuksi vielä complete manualiin...

        tldr grep

<img width="1214" height="675" alt="image" src="https://github.com/user-attachments/assets/32a472a8-d4a2-499a-acfd-5de49cb959f6" />

`tldr` tuntuu puolestaan aika suppealta.

