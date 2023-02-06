# LinuxPalvelimet-h6-Based
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## x) 
### Getting started - Apache2
- URL: uniform resource locator vastaa siitä, mikä palvelimella oleva resurssi näytetään selaimen käyttäjälle
- Virtual hostien avulla voidaan pyörittää useampaa kuin yhtä sivua serverillä.
- DocumentRoot kertoo missä hakemistossa sijaitsee sivuston resurssit
### Name-based Virtual Host Support
- Virtual hostien avulla yhdellä ip:llä voi olla useampi host.
- ServerName kannaattaa aina määritellä, koska muuten sivu perii serverin nimen perus serveri configuraatiosta
## a) + b) 
Muuttaaksemme apachen etusivua, tulee meidän luoda uusi conf tiedosto sivua varten.

    sudoedit /etc/apache2/sites-available/frontpage.conf
    
![confsivu](https://user-images.githubusercontent.com/112503770/216899160-9ae6c132-429c-4370-ad86-2075fd1b17ef.png)


Nyt voimme ajaa komennot, joilla otamme käyttöön luomamme conf tiedoston, kytkemme vanhan default conf tiedoston pois päältä ja käynnistämme apachen uudelleen.

    sudo a2aensite frontpage.conf
    sudo a2dissite 000-default.conf
    sudo systemctl restart apache2
    
![jokuvika](https://user-images.githubusercontent.com/112503770/216899307-c5a30576-6a8d-4de6-a4e4-a173b5d0bb4a.png)

    
Ajettuani kommenot huomasin että apache ei suostunut käynnistymään, joten aloitin vianhakuprosessin ajamalla komennon `sudo tail -1 var/log/apache2/error.log`, josta sain tulokseksi:

![errorlogi](https://user-images.githubusercontent.com/112503770/216958915-01faebb3-1025-4d61-9dbd-0397e247d015.png)

Login tieto on varsin epäselvää, mutta googlettamalla varmasti lokin sisältö aukenisi enemmän. Laiskana ajoin toisen komennon `sudo apache2ctl configtest`, jolla sain paljon luettavamman tuloksen.

![configtestlogi](https://user-images.githubusercontent.com/112503770/216959230-c7fdad53-3da6-4925-966a-1e0f2ddd8d59.png)

Katsomalla configtestin tulosta ilmenee, että edellä tehty .conf tiedosto oli määritelty väärin ja lopputagi oli virheellinen. Saman tiedon saa myös ajamalla apachen ehdottaman komennon:
    
    sudo systemctl status apache2
    
![vika_raportti](https://user-images.githubusercontent.com/112503770/216899348-b64c082d-0265-43e5-8a16-52a4f2651af3.png)
 
 ![vian_syy](https://user-images.githubusercontent.com/112503770/216899372-42151216-359a-455d-b12b-4166e58f8316.png)
  
Status ruutua navigoimalla löytää tiedon, että olin kirjoittanut conf tiedostoni hieman väärin, joten korjaan tiedostossa väärin kirjoitetun virtualhost lopputagin komennoilla:

    sudoedit /etc/apache2/sites-available/frontpage.conf
    sudo systemctl restart apache2
    
Luomamme conf on nyt käytössä, joten voimme luoda sitä vastaavan nettisivun kansioon, jonka kirjoitimme conf tiedostoon.

    cd
    mkdir sites
    micro index.html
    
![apach1](https://user-images.githubusercontent.com/112503770/216899623-7a5d49bf-8dc4-4c70-909a-8fd8feb3a2e1.png)
 
Testataan että sivu toimii:

    curl "http://localhost"

![kaikki_ok](https://user-images.githubusercontent.com/112503770/216899555-93698978-80ed-4a16-baae-6277352e4ceb.png)


## Lähteet

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://httpd.apache.org/docs/2.4/getting-started.html
    https://httpd.apache.org/docs/current/vhosts/name-based.html
    
