# Salataampa

Tiivisteitä:

- Let's Encrypt käyttää ACME-protokollaa (Automatic Certificate Management Environment) keskustellakseen weppipalvelimen kanssa
- Sieltä sitten tsekataan, kuka omistaa palvelimen haasteiden avulla (esim. laita tämmönen merkkijono sivustollesi tähän polkuun yms.)
- Jos haasteet läpäistään, niin CA (Certificate Authority) myöntää TLS-sertifikaatin

Tämän viikon läksyt ovat kovin lyhyet verratuna aikaisempiin, kun ei tarvitse enään käyttää tuota Lego-ohjelmaa sertifikaatin hommaamiseen, vaan Certbot hoitaa kaiken puolesta.

    sudo ufw allow 443/tcp
    sudo apt-get install certbot python3-certbot-apache
    sudo certbot --apache --domains lofving.me.com, www.lofving.me.com


<img width="1103" height="630" alt="image" src="https://github.com/user-attachments/assets/43d523b8-6d5a-4bd2-a9bd-3119a37515eb" />

