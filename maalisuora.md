# Maalisuora!

## Hello world kolmella kielellä


### Java

Ladataan java:

    sudo apt install jdk-default

[Teron ohjeita kurkkasin](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/) ja koodasin javalla hello world:

    micro helloworld.java

    public class HelloWorld
    {
     public static void main(String[] args)
     {
     System.out.print.in("Hello world!")
     }
    }    

Mutta mites tää osoittautuikaan näin hankalaksi kun tulee erroria errorin perään:

<img width="1076" height="481" alt="Screenshot from 2025-10-06 22-28-50" src="https://github.com/user-attachments/assets/b9b797a3-04a9-4a80-be4f-9de5d85166b8" />

Ekaksi puuttui `;` syntaksista.
Sitten tuli error: `class HelloWorld is public, should be declared in a file HelloWorld.java`
Seuraavan errorin kanssa käytin liikaa aikaa: `cannot find symbol` viitaten System.out.print.In
kikkailin syntaksin kanssa jonkin verran mutta erorri toistui... Oli pakko hakea apua [stackoverflowista](https://stackoverflow.com/questions/13811020/error-class-x-is-public-should-be-declared-in-a-file-named-x-java) ja sieltähän se vastaus tulikin ja voi pojat kun tuli hölmö olo.
Eli se ei ollutkaan print.In vaan print.ln... Damn. Ei siis ollut Teron ohjeissa väärin vaan itse pitäisi käydä vaan Specsaversillä.

<img width="512" height="143" alt="image" src="https://github.com/user-attachments/assets/94a5053e-e115-4e79-81f8-00e1ad2e6a02" />


### Python

        micro helloworld.py
        
        print("Hello world!")

        python3 helloworld.py

<img width="530" height="63" alt="image" src="https://github.com/user-attachments/assets/fd9e6e7b-ace3-4aff-8b27-2391a8bfac63" />

Ihanan selkeä ton Javan jälkeen.

## C

Testataas vielä C:llä. Tätä tuli pienen hetken opiskeltua niin katsotaan muistanko ulkomuistista.

        micro helloworld.c

        #include <stdio.h>

        void main()
        {
         printf("Hello world!");
        }

        gcc helloworld.c

Tässä unohdin lisätä `-o` eli outputin tuon `gcc helloworld.c` perään, joka kertoo kääntäjälle (gcc), minkä nimiseksi käännetty suoritettava tiedosto nimetään.
Jos sitä ei ilmoita, niin se luo oletuksena tiedoston nimeltä `a.out`

<img width="1825" height="573" alt="image" src="https://github.com/user-attachments/assets/7a634e85-6b78-4b58-ba2e-c975148eef98" />

Tässä kurkkasin mitä `a.out` pitää sisällään ja se on juurikin se käännetty binaaritiedosto koska näyttää tekstieditorissa siansaksalta.
Kun sen ajaa `./a.out`, niin sieltähän se Hello world! tuli.

## Yhteinen komento

Lisätään shebang-rivi skriptin alkuun, joka kertoo Linuxille, millä ohjelmalla tiedosto ajetaan.

        #! /usr/bin/env python3

        chmod +x infoa.py

        sudo cp infoa.py /usr/local/bin/

Ja tämän jälkeen jokaisen käyttäjän pitäisi pystyä ajamaan skripti mistä tahansa ja ilman ylimääräistä python3 -alkua.

Testataan luomalla uusi käyttäjä

        sudo adduset testi

        su - testi

<img width="1004" height="101" alt="image" src="https://github.com/user-attachments/assets/7157b121-cf16-443a-a0ce-3f6c6a3583b5" />

No olisihan se ollut liian helppoa jos ykkösellä ois mennyt purkkiin. Katsotaas mistä kiikastaa.

<img width="1004" height="117" alt="image" src="https://github.com/user-attachments/assets/148410e2-ab4c-41f1-9dcc-bff0644a2e73" />

Jostain syystä se ei digannut tuosta `env` -komennosta shebangissä. Python3 kuitenkin löytyy `/usr/bin`-hakemistosta niin otin sen poies. [Täältä](https://stackoverflow.com/questions/21612980/why-is-usr-bin-env-bash-superior-to-bin-bash) luin kuinka se `env` olisi hyvä lisätä shebangiin. Eli jos oikein ymmärsin niin se automaattisesti etsii sen pythonin käyttäjän `PATH`ista. __EDIT:__ jälleen kerran huomaan että syntaksi on mun pahin vihollinen. Mulla oli ollut yksi ylimääräinen välilyönti shebangissa, joten se ei ollut toiminut...


<img width="916" height="293" alt="image" src="https://github.com/user-attachments/assets/52c20178-31c3-4b43-818b-6ea532fd195f" />

Koodi näytti ohjelmassa tältä:

<img width="761" height="432" alt="image" src="https://github.com/user-attachments/assets/64737d70-ff0e-4a56-ae8e-b4894810ac62" />

## Vanha labraharjoitus soveltavasti

[Täältä](https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/) poimin tehtäviä tehtäväksi.

Uudelta ja mielenkiintoiselta vaikutti tuo Django kehitysympäristön asennus ja sen tutkiminen, joten lähdin sitä työstämään. En ole siis aikaisemmin koskenutkaan siihen.

Käytin tehtävien teossa ohjeena [W3Schoolia](https://www.w3schools.com/django/django_create_virtual_environment.php).

Eli tarvitaan Pythonin package installeri nimeltä `pip`

        sudo apt install pip

Seuraavaksi luodaan virtuaaliympäristö projektille

        mkdir djhatut
        cd djatut
        python3 -m venv djhats

<img width="817" height="348" alt="image" src="https://github.com/user-attachments/assets/387f8b99-a139-492f-8301-b45ad262a94a" />

OK. Latasin tuon, poistin sen virheellisen hakemiston alihakemistoineen `rm -r djhats` ja ajoin uudestaan.
Aktivoin ympäristön:

        source djhats/bin/activate

<img width="811" height="201" alt="image" src="https://github.com/user-attachments/assets/f6c1ae1f-9ddf-49fb-83d2-4724d1f3bcb2" />

Tuo aktivointi täytyy tehdä joka kerta kun haluaa työskennellä Django-projektin parissa. (W3School.2025)

Nyt sitten pääsin lataamaan Django. Se tehdään, kun ollaan tuossa ympäristössä.

        python -m pip install Django

Startataan projekti

        django-admin startproject djangohats
        cd djangohats
        python manage.py runserver

Tämän jälkeen voi käydä katsomassa miltä projekti näyttää selaimessa 127.0.0.1:8000 

<img width="814" height="408" alt="image" src="https://github.com/user-attachments/assets/bacaa895-9bff-41c7-ae12-7673d50452b4" />

Seuravaaksi luodaan se hattuäppi Djangoon.

        python manage.py startapp hats

Tässä vaiheessa siirryin käyttämään tekoälyä mentorinani, sillä W3Schools keskittyi Hello Worldiin. ChatGPT (OpenAI, 2025) kävi läpi seuraavat askeleet, kun iskin sille promptiksi tehtävänannon ja että olen nyt siinä vaiheessa, että hattuäppi löytyy jo.

Ensimmäiseksi käski rekisteröimään sovelluksen `settings.py`-tiedostossa

        micro djhats/djangohats/djangohats/settings.py

Ois kyllä pitänyt nimetä vähän eri nimisiksi näitä ympäristöjä :D

<img width="772" height="274" alt="image" src="https://github.com/user-attachments/assets/cdc9a532-c095-4571-aefe-06d3818169a9" />

Settingseistä etsittiin `INSTALLED_APPS`-kohta ja sinne lisättiin `hats` ChatGPT (OpenAI, 2025)

Seuraavaksi luotiin tietorakenne `models.py`-tiedostoon:

<img width="927" height="262" alt="image" src="https://github.com/user-attachments/assets/4855415d-b688-4017-8b43-36a63b830fdf" />

Sitten lisättiin kyseinen malli admin-paneeliin

        micro djhats/djangohats/hats/admin.py
        from django.contrib import admin
        from .models import Hat

        admin.site.register(Hat)

Lopuksi päivitetään tietokanta ja luodaan ylläpitäjä

        python manage.py makemigrations
        python manage.py migrate
        python manage.py createsuperuser

Käynnistetään palvelin ja avataan selain

        python manage.py runserver
        selaimeen 127.0.0.1:8000/admin

Tuolta päästiin sitten kirjautumaan sisään luoduilla tunnuksilla ja käsittelemään hattuja.

<img width="949" height="451" alt="image" src="https://github.com/user-attachments/assets/cf9b36a5-1f2e-4d2c-ba50-2eda098ce419" />

Olihan tää nyt oikein suoraviivaista kun seurasi W3Schoolin ja ChatGPT:n ohjeita, mutta ihan hyvä ensimaku Djangoon.
        
## Lähteet

https://stackoverflow.com/questions/13811020/error-class-x-is-public-should-be-declared-in-a-file-named-x-java

Tero Karvinen. 2018. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

Stackoverflow. Variable out of type printstream error occured .2015. Haettu 6.10.2025. https://stackoverflow.com/questions/9298980/variable-out-of-type-printstream-error-occured

W3Schools. Django. (n.d). Haettu 7.10.2025. https://www.w3schools.com/django/django_create_virtual_environment.php

