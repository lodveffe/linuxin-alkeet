# Salataampa

Tiivisteitä:

- Let's Encrypt käyttää ACME-protokollaa (Automatic Certificate Management Environment) keskustellakseen weppipalvelimen kanssa
- Sieltä sitten tsekataan, kuka omistaa palvelimen haasteiden avulla (esim. laita tämmönen merkkijono sivustollesi tähän polkuun yms.)
- Jos haasteet läpäistään, niin CA (Certificate Authority) myöntää TLS-sertifikaatin

Tämän viikon läksyt ovat kovin lyhyet verrattuna aikaisempiin, kun ei tarvitse enään käyttää tuota Lego-ohjelmaa sertifikaatin hommaamiseen, vaan Certbot hoitaa kaiken puolesta.

Nämä vain terminaaliin:

    sudo ufw allow 443/tcp
    sudo apt-get install certbot python3-certbot-apache
    sudo certbot --apache --domains lofving.me.com, www.lofving.me.com

ja voilá!

<img width="745" height="234" alt="Screenshot from 2025-09-29 22-43-10" src="https://github.com/user-attachments/assets/176f0ee1-a288-4efb-851c-54a22fcf1b4a" />

Käydään vielä SSL Labsin kautta katsomassa, kuinka hyvin TLS-asetukset ovat konfiguroitu. Siitä saadaan arvosana A+ ja F -väliltä.

<img width="1103" height="630" alt="image" src="https://github.com/user-attachments/assets/43d523b8-6d5a-4bd2-a9bd-3119a37515eb" />

Koitetaan saada se A+. [Tältä sivulta](https://www.inmotionhosting.com/support/website/ssl/disable-tls-versions/) löysin ohjeita kuinka poistetaan käytöstä vanhentuneet TLS-versiot.

        sudo micro /etc/apache2/sites-available/lofving.me-le-ssl.conf

ja sinne lisätään tuo alhaalla oleva SSLProtocol rivi. Lisäsin myös [Apachen how-to-sivuilta](https://httpd.apache.org/docs/trunk/ssl/ssl_howto.html) nuo muutamat rivit Strong Encryption-kohdan alta, eli

        SSLProtocol         all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
        SSLCipherSuite HIGH:!aNULL:!MD5 #tällä poistetaan heikot MD5 hashit käytöstä
        SSLHonorCipherOrder on
        SSLCompression      off
        SSLSessionTickets   off


<img width="797" height="540" alt="Screenshot from 2025-09-30 12-06-28" src="https://github.com/user-attachments/assets/2ade422a-f4b3-4fdf-b918-6f346b5a22dc" />

Noh SSLLabsin tulos näyttää edelleen arvosanaksi A:n. Tulipahan yritettyä!

## Lähteet:

[Let's Encrypt 2025, How it works](https://letsencrypt.org/how-it-works/)

[Apache2 2025](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample)

[InMotionHosting 2022](https://www.inmotionhosting.com/support/website/ssl/disable-tls-versions/)

[SSLLabs 2025](https://www.ssllabs.com/ssltest/analyze.html?d=lofving.me)
