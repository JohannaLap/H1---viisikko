# H1---viisikko
## X) Tiivistelmä

## b) Saltin asennus
Ensiksi päivitin  `sudo apt-get update`.

Tämän jälkeen 
'sudo mkdir -p /etc/apt/keyrings'
'sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg'
'echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list'

Tarkistin mikä versio on käytössä `sudo salt-call --version`.
![Tarkistin mikä versio on käytössä `sudo salt-call --version`.](https://github.com/JohannaLap/H1---viisikko/blob/5bac7a744ed3abbeaca270ce3e7ea78e603e10e1/salt%20call%20version.png)

## c) Viisi tärkeintä
Saltin viisi tärkeintä tilafunktiota: pkg, file, service, user ja cmd.

'sudo salt-call --local -l info state.single pkg.installed tree' 
Tämä näyttää, että paketti tree asennettiin onnistuneesti
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/pkg.installed.png)

'sudo salt-call --local -l info state.single pkg.removed tree'
Vastaavasti tällä komennolla saatiin tieto, että paketti tree on poistettu. 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/pkg.removed.png)

'sudo salt-call --local -l info state.single file.managed /tmp/moikka' 
Tällä komennolla luotiin onnistuneesti uusi tiedostopolku. Kuvasta nähdään, että tiedosto on tyhjä. 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/filemanaged.png)

'sudo salt-call --local -l info state.single file.managed /temp/hello contents="foo"'
Tämä puolestaan luo tiedostopolkuun temp/hello sisälle teksin foo.

Tässä myös esimerkki tiedostopolun poistamisesta: 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/file%20managed%20absent.png)

Tässä esimerkki apache2 katsomisesta. Kuvasta näkyy, että apache2 on jo käynnissä onnistuneesti.
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/commit/90a586dfcaa6d7dd5afcdaa2c1bd4e04ba7a9f3b)

'sudo salt-call --local state.single user.present name=johanna'
Komennolla saadaan lisättyä uusi käyttäjä. Tässä kuvassa nähdään että käyttäjä on jo olemassa, eikä muutoksia tarvinnut siis tehdä. 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/user%20present.png)

Tässä vielä toinen esimerkki, jossa näkyy uuden käyttäjän lisääminen, jota ei vielä ole olemassa.
![kuvateksti] (https://github.com/JohannaLap/H1---viisikko/blob/main/single%20user%20present.png)

Ja vielä esimerkki käyttäjän poistamisesta
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/user%20absent.png)

Sitten vielä cmd. Tässä touch komennolla luodaan tidosto /tmp/foo jos sitä ei vielä ole. Kuten kuvasta nähdään tiedosto oli jo olemassa.

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/1e333f1eed6ab3b361cda1def620e44b0d0b36c2/cmd%20run.png)

## d) Idempotentti
Idempotentilla tarkoitetaan komennon antavan aina saman lopputuloksen. Lopputulos ei siis ole riippuvainen siitä, kuinka monesti komento suoritetaan. 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/idempotentti.png)

## e) Herra-orja
Tässä komento jolla testasin toimivuuden
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/yhteystestiping.png)

