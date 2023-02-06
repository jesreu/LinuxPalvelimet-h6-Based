# LinuxPalvelimet-h6-Based
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## x) 
### Getting started - Apache2

### Name-based Virtual Host Support

## a) + b) 
Muuttaaksemme apachen etusivua, tulee meidän luoda uusi conf tiedosto sivua varten.

    sudoedit /etc/apache2/sites-available/frontpage.conf
    
Kuve

Nyt voimme ajaa komennot, joilla otamme käyttöön luomamme conf tiedoston, kytkemme vanhan default conf tiedoston pois päältä ja käynnistämme apachen uudelleen.

    sudo a2aensite frontpage.conf
    sudo a2dissite 000-default.conf
    sudo systemctl restart apache2
    
Ajettuani kommenot huomasin että apache ei suostunut käynnistymään, joten aloitin vian haku prosessin ajamalla komennon `sudo tail -1 var/log/apache2/error.log`, mutta se ei antanut juurikaan järkevää tulosta. Ajamalla apachen ehdottaman komennon:
    
    sudo systemctl status apache2
    
Kuve kuve
    
Sain status ruutua navigoimalla tiedon, että olin kirjoittanut conf tiedostoni hieman väärin, joten korjaan tiedostossa ilmenneen virheen komennoilla:

    sudoedit /etc/apache2/sites-available/frontpage.conf
    sudo systemctl restart apache2
    
Luomamme conf on nyt käytössä, joten voimme luoda sitä vastaavan nettisivun kansioon, jonka kirjoitimme conf tiedostoon.

    cd
    mkdir sites
    micro index.html
    
Testataan että sivu toimii:

    curl "http://localhost"

kuve

## Lähteet

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://httpd.apache.org/docs/2.4/getting-started.html
    https://httpd.apache.org/docs/current/vhosts/name-based.html
    
