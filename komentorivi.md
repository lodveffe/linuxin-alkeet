# Komentorivin perusteet

Peruskomentoja:

[https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited](laitan Teron cheatsheetin tänne)

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
