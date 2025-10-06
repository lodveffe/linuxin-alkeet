# Maalisuora!

## Hello world kolmella kielellä

### Python


### Java

Ladataan java:

    sudo apt install jdk-default

[Teron ohjeiden mukaan](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/) koodataan javalla hello world:

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
Eli se ei ollutkaan print.In vaan print.ln... Damn.

## Lähteet

https://stackoverflow.com/questions/13811020/error-class-x-is-public-should-be-declared-in-a-file-named-x-java

https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

https://stackoverflow.com/questions/9298980/variable-out-of-type-printstream-error-occured
