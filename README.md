# H1---viisikko
## X) Tiivistelmä
Tärkeimpiä funktioita ovat pkg, file, service, user ja cmd. 
Ennen saltin asennust on hyvä muistaa päivittää `sudo apt-get update` .
Päivitttämsien jälkeen saltin asennus on helppo tehdä komennolla `sudo apt-get -y install salt-minion`
Komennoilla `salt-call --local` voidaan testata ja hallita paketteja lokaalisti.

Saltstackin avulla useien tietokoneiden hallinta samanaikaisesti on mahdollista. 
Masterin asennus tapahtuu seuraavilla komennoilla :
 `sudo apt-get update`
 `sudo apt-get -y install salt-master`

Minionin asennus seuraavasti: 
 `sudo apt-get update`
 `sudo apt-get -y install salt-minion`

 Minionin käynnistyksen jälkeen avain täytyy hyväksyä. Ja lopuksi on hyvä testata että yhteys masterin ja minionin välillä toimii toivotusti. 

## b) Saltin asennus
Ensiksi päivitin  `sudo apt-get update`.

Tämän jälkeen 
`sudo mkdir -p /etc/apt/keyrings`
`sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg`
`echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list`

Tarkistin mikä versio on käytössä `sudo salt-call --version`.

![Tarkistin mikä versio on käytössä `sudo salt-call --version`.](https://github.com/JohannaLap/H1---viisikko/blob/5bac7a744ed3abbeaca270ce3e7ea78e603e10e1/salt%20call%20version.png)

## c) Viisi tärkeintä
Saltin viisi tärkeintä tilafunktiota: pkg, file, service, user ja cmd.

Tämä näyttää, että paketti tree asennettiin onnistuneesti
`sudo salt-call --local -l info state.single pkg.installed tree` 

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/pkg.installed.png)

Vastaavasti tällä komennolla saatiin tieto, että paketti tree on poistettu.
`sudo salt-call --local -l info state.single pkg.removed tree`
 
![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/pkg.removed.png)

Tällä komennolla luotiin onnistuneesti uusi tiedostopolku. Kuvasta nähdään, että tiedosto on tyhjä. 
`sudo salt-call --local -l info state.single file.managed /tmp/moikka`

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/filemanaged.png)

Tämä puolestaan luo tiedostopolkuun temp/hello sisälle teksin foo.
`sudo salt-call --local -l info state.single file.managed /temp/hello contents="foo" `


Tässä myös esimerkki tiedostopolun poistamisesta: 

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/file%20managed%20absent.png)

Tässä esimerkki apache2 katsomisesta. Kuvasta näkyy, että apache2 on jo käynnissä onnistuneesti.
![tekstiä](https://github.com/JohannaLap/H1---viisikko/blob/main/Apache%20running.png)

Komennolla saadaan lisättyä uusi käyttäjä. Tässä kuvassa nähdään että käyttäjä on jo olemassa, eikä muutoksia tarvinnut siis tehdä. 
`sudo salt-call --local state.single user.present name=johanna`


![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/user%20present.png)

Tässä vielä toinen esimerkki, jossa näkyy uuden käyttäjän lisääminen, jota ei vielä ole olemassa.

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/single%20user%20present.png)

Ja vielä esimerkki käyttäjän poistamisesta

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/user%20absent.png)

Sitten vielä cmd. Tässä touch komennolla luodaan tidosto /tmp/foo jos sitä ei vielä ole. Kuten kuvasta nähdään tiedosto oli jo olemassa.

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/1e333f1eed6ab3b361cda1def620e44b0d0b36c2/cmd%20run.png)

## d) Idempotentti
Idempotentilla tarkoitetaan komennon antavan aina saman lopputuloksen. Lopputulos ei siis ole riippuvainen siitä, kuinka monesti komento suoritetaan. 

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/idempotentti.png)

## e) Herra-orja

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/whoami.png)

![kuvateksti](https://github.com/JohannaLap/H1---viisikko/blob/main/testi.png)


Lähteet: Karvinen, 2023: Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/
         Karvinen, 2018: Salt Quickstart-salt stack master and slave on ubuntu linux. https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-    slave-on-ubuntu-linux/

