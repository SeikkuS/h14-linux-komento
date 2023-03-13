# h14-linux-komento

Aloitin tehtävän tekemisen 13.3.2023 klo 8.58.

## a) Uusi komento Bashilla

Päätin tehdä bashilla komennon, joka tulostaa päivämäärän ja kellonajan. Aloitin tekemällä touch -komennolla uuden tiedoston nimeltä bashcommand, jonka jälkeen muokkasin tiedostoa ja kirjoitin siihen "date":

      touch bashcommand
      micro bashcommand

![kuva](https://user-images.githubusercontent.com/105205141/224630109-561a73e2-2d22-47fc-9279-7f2402eea87e.png)

Tallensin muutokset ja poistuin tiedostosta.

Tämän jälkeen tein tiedostosta käynnistettävän (executable) käyttäen chmod -komentoa:

    chmod +x bashcommand

Sitten siirsin tiedoston järkevään hakemistoon, josta se pystytään runaamaan helposti ja yksinkertaisesti riippumatta, missä hakemistossa ollaan:

    sudo mv bashcommand /usr/local/bin/
    
Jonka jälkeen pystyn toteuttaa komennon seuraavasti:

![kuva](https://user-images.githubusercontent.com/105205141/224630994-77de1f51-bf2f-4830-b77b-70cb7a854450.png)

Kuvassa nähdään, että päivämäärä on oikein ja että kellonaika sekä aikavyöhyke ovat oikein.

## b) Uusi komento Pythonilla (klo 9.08)

Tehdäkseni samanlaisen komennon pythonilla, aloitan ensin samalla tavalla luomalla tiedoston ja muokkaamalla sitä microlla:

      touch pycommand
      micro pycommand
      
![kuva](https://user-images.githubusercontent.com/105205141/224631688-582271ff-41cc-4b71-8813-f4156321780a.png)

Sitten käytän samaa chmod-komentoa tiedostoon:

      chmod +x pycommand
      
Päätin myös siirtää tämän helpompaan hakemistoon:

    sudo mv pycommand /usr/local/bin/
    
Kokeillessani käynnistää uuden komentoni, huomasin ettei ohjelmani löydä pythonia hakemistosta /usr/bin/env - tutkittuani tajusin, että kyseessä on siis python2 eikä python3, joten menin tiedostoon ja muokkasin halutun python version 3:ksi.

![kuva](https://user-images.githubusercontent.com/105205141/224632639-e1792300-eb5c-47af-a773-c384600e35e7.png)

Tämän jälkeen komento toimii halutulla tavalla, kun kirjoitan:

    pycommand
    
![kuva](https://user-images.githubusercontent.com/105205141/224632804-b76da815-2e6b-4f2c-808b-906e4cfed767.png)

## c) Komento joka vaikuttaa moneen tiedostoon (klo 9.17)

Päätin tehdä uuden tiedoston samalla tyylillä ja microttaa siihen:

    touch modifyfiles
    micro modifyfiles
    
Tänne kirjoitin:
    
    #!/bin/bash
    find . -type f -exec grep -q 'foo' {} \; -print0 | xargs -0 sed -i 's/foo/bar/g'
    
Tässä käytetään find-komentoa etsimään kyseisessä hakemistossa kaikki tiedostot, jotka sisältävät "foo"-merkkijonon. Sen jälkeen xargs lähettää listan tiedostoista sed-komennolle, joka korvaa kaikki foo-merkkijonot bar-merkkijonolla. (-print0 ja xargs -0 käsittelevät tiedostonimiä jotka sisältävät erikoismerkkejä)

Tein chmod +x -komennon vielä tiedostolle.

Tämän jälkeen tein esimerkkitiedostoja, joissa lukee erilaisia merkkijonoja sisältäen "foo" eri paikoissa. Siirsin kaikki esimerkkitiedostot sekä komennon uuteen hakemistoon:

![kuva](https://user-images.githubusercontent.com/105205141/224635294-6cf33a1b-1067-4a4b-b955-e0c0008bd079.png)

![kuva](https://user-images.githubusercontent.com/105205141/224635234-9e18103d-2a9a-4978-9954-435dd6e6ebe2.png)

Kokeilin pyörittää komentoa:

Huomasin että /usr/local/bin/ tiedostossa ei voida pyörittää komentoa, ellei käytetä sudoa:

![kuva](https://user-images.githubusercontent.com/105205141/224635751-214c8083-f732-4be3-99bc-659274fe91f6.png)

avasin esimerkkitiedoston:

![kuva](https://user-images.githubusercontent.com/105205141/224635896-fe4f1f64-ed97-4cee-b5c3-8693ce4f2ae7.png)

voidaan todeta vaikka raportissa ei nyt ollutkaan alkuperäisestä kuvaa, ettei tiedostossa missään kohtaa lue bar.
Katson toisenkin.

![kuva](https://user-images.githubusercontent.com/105205141/224636042-94c2bd60-8584-4fb3-8657-9532c0ccd0f4.png)

Tässä nähdään, että "foo" ei tarvitse olla erikseen vaan se voi olla muiden merkkien ympäröimänä ja komento silti löytää merkkijonon "foo" välistä.

Lopetin tehtävän klo 9.36.


