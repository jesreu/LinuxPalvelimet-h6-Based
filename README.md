# LinuxPalvelimet-h6-Based
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## x) 
### Getting started - Apache2

### Name-based Virtual Host Support

## a) + b) 

    sudoedit /etc/apache2/sites-available/frontpage.conf
    sudo a2aensite frontpage.conf
    sudo a2dissite 000-default.conf
    sudo systemctl restart apache2
    
    sudo tail -1 var/log/apache2/error.log
    sudo systemctl status apache2
    
    sudoedit /etc/apache2/sites-available/frontpage.conf
    sudo systemctl restart apache2
    
    cd
    mkdir sites
    micro index.html
    curl "http://localhost"

## Lähteet

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://httpd.apache.org/docs/2.4/getting-started.html
    https://httpd.apache.org/docs/current/vhosts/name-based.html
    
