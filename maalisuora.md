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


## Lähteet

https://stackoverflow.com/questions/13811020/error-class-x-is-public-should-be-declared-in-a-file-named-x-java

https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

https://stackoverflow.com/questions/9298980/variable-out-of-type-printstream-error-occured
