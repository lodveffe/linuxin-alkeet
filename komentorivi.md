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


