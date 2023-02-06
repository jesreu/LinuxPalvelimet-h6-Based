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
    
![confsivu](https://user-images.githubusercontent.com/112503770/216899160-9ae6c132-429c-4370-ad86-2075fd1b17ef.png)



Nyt voimme ajaa komennot, joilla otamme käyttöön luomamme conf tiedoston, kytkemme vanhan default conf tiedoston pois päältä ja käynnistämme apachen uudelleen.

    sudo a2aensite frontpage.conf
    sudo a2dissite 000-default.conf
    sudo systemctl restart apache2
    

![jokuvika](https://user-images.githubusercontent.com/112503770/216899307-c5a30576-6a8d-4de6-a4e4-a173b5d0bb4a.png)

    
Ajettuani kommenot huomasin että apache ei suostunut käynnistymään, joten aloitin vianhakuprosessin ajamalla komennon `sudo tail -1 var/log/apache2/error.log`, mutta se ei antanut juurikaan järkevää tulosta. Ajamalla apachen ehdottaman komennon:
    
    sudo systemctl status apache2
    
![vika_raportti](https://user-images.githubusercontent.com/112503770/216899348-b64c082d-0265-43e5-8a16-52a4f2651af3.png)
 
 ![vian_syy](https://user-images.githubusercontent.com/112503770/216899372-42151216-359a-455d-b12b-4166e58f8316.png)
  
Sain status ruutua navigoimalla tiedon, että olin kirjoittanut conf tiedostoni hieman väärin, joten korjaan tiedostossa väärin kirjoitetun virtualhost lopputagin komennoilla:

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
    
