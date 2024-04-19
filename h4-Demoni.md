# h4 Demoni

Neljännen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## x) Lue ja tiivistä

### 1. Karvinen 2023: Salt Vagrant – automatically provision one master and two slaves 

- Infra as Code – Your wishes as a text file

  - Luodaan hakemisto tilamoduulille, esim. moduuli hello -> luodaan hakemisto /srv/salt/hello
  
  - Tähän hakemistoon luodaan init.sls-tiedosto, johon kirjoitetaan suoritettavaksi halutut toiminnot YAML-merkintäkielellä (infraa koodina)
  
  - hello-moduuli suoritetaan kaikille orjille komennolla ```sudo salt '*' state.apply hello```

 - top.sls – What slave runs what states

   - top.sls-tiedostoa käytetään määrittämään mitkä moduulit suoritetaan milläkin orjakonella
  
   - Hakemistoon /srv/salt/hello luodaan top.sls-tiedosto
  
   - Esim. jos hello-tilamoduuli halutaan suorittaa kaikilla orjilla, top.sls-tiedostoon kirjoitetaan:

     ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e63d2abb-0cb9-46eb-bc5b-968d17cb4057)
  
   - Komennolla ```sudo salt '*' state.apply``` suoritetaan top.sls-tiedoston mukaiset tilamoduulit

### 2. SaltProject 2024: Salt contributors – Salt overview 

- Rules of YAML

  - YAML-renderöijä on oletuksena monissa Saltin käyttämissä tiedostoissa: se kääntää YAML-tietorakenteen Python-tietorakenteeksi Saltin käyttöön
  
  - Tieto jäsennellään pareina (key: value)
  
  - Kirjainkoolla on merkitystä
  
  - Käytä välilyöntiä (ei tabulaattoria) sisennysten tekemiseen
  
  - Kommenteiksi tarkoitetut rivit aloitetaan #-merkillä

- YAML simple structure

  - YAML koostuu kolmesta peruselementistä: scalars, lists ja dictionaries
    
  - esim.

  ![image](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/abf7fea9-0793-4329-9e59-33850076b0d0)

- Lists and dictionaries – YAML block structures

  - YAML koostuu lohkorakenteista
  
  - Sisennys määrittää kontekstin
  
  - Kokoelmissa (lists & dictionaries) jokainen merkintä osoitetaan väliviivalla ja välilyönnillä ("- ")
 
### 3. Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port 

- Saltin avulla pystytään hallitsemaan useita demoneja 

- package-file-service -malli

  - ohjelman asentaminen (package)
    
  - konfiguraatiotiedoston korvaaminen (file)
    
  - demonin uudelleenkäynnistäminen (service) 

- SSH-palvelinportin muuttaminen Saltin avulla 

  - luodaan herra-orja-arkkitehtuuri virtuaalikoneille 

  - luodaan herralle tilamoduuli (sshd.sls) 

  - luodaan herralle konfiguraatiotiedoston kopio (sshd_config), jossa muokataan SSH-porttinumeroa 

  - ajetaan tila kaikille orjille: ```sudo salt '*' state.apply sshd```
 
### 4. Salt tilafunktioiden ohjeet (Salt-ohjelmiston sisäinen manuaalisivu, sys.state_doc)

- pkg 

  - johdanto: ohjelmistopakettien hallinta Saltilla

  - pkg.installed: varmistetaan, että nimetty ohjelmistopaketti on asennettu

  - pkg.purged: varmistetaan, että nimettyä ohjelmistopakettia ei ole asennettu 

  - pkgs: nimetään useampi ohjelmistopaketti toiminnon kohteeksi

- file 

  - johdanto: toiminnot tiedostojen, hakemistojen ja symlinkkien hallitsemiseen / Saltilla voidaan manipuloida aggressiivisesti järjestelmän tiedostoja useilla eri tavoilla

  - file.managed: nimetyn tiedoston hallinta, esimerkiksi lataaminen herrasta orjaan 

  - file.absent: varmistaa, että nimetty tiedosto tai hakemisto puuttuu -> jos se on olemassa, se poistetaan 

  - file.symlink: luodaan symbolinen linkki haluttuun tiedostoon 

- service 

  - johdanto: järjestelmään/palveluihin liittyvät ohjeet 

  - service.running: nimetyn palvelun toiminnan / käynnissäolon varmistaminen 

  - service.dead: varmistetaan, että tietty palvelu on pysäytetyssä tilassa / pysäytetään palvelu, mikäli se on toiminnassa

  - enable: nimetyn palvelun käyttöönotto käynnistyksen yhteydessä
 
## a) Hello SLS!

Tässä tehtävässä käytin aiemmassa h2-kotitehtävässä laatimaani virtuaalikonetta t001.

### Hei maailma -tila tekstitiedostona

- Loin hello-tilamoduulia varten hakemiston komennolla ```sudo mkdir -p /srv/salt/hello```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/68922ad0-407d-49c6-b677-168d71294b6a)

- Siirryin kyseiseen hakemistoon ja loin sinne tiedoston init.sls.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e2995363-7afc-4091-b8ee-b1d57cf473bf)

- Loin tilamoduulin, jossa tmp-hakemistoon luodaan hellosls-niminen tiedosto, jos sitä ei ole entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1b6c8ada-7d33-4602-9646-02d3d4c9baf7)

- Suoritin hello-tilamoodulin paikallisesti komennolla ```sudo salt-call --local state.apply hello```. /tmp/hellosls-tiedosto luotiin onnistuneesti, koska sitä ei ollut entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6cf4b12b-17e7-4542-b7d7-9bc03e32306c)

- Tarkistin vielä tiedoston onnistuneen luonnin siirtymällä tmp-hakemistoon.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1c9eeafd-77f7-431c-bc0c-d43cbd09b40e)

## b) Top

Tässä tehtävässä käytin aiemmassa h2-kotitehtävässä laatimiani virtuaalikoneita t001 ja t002.

### Useiden tilamoduulien suorittaminen orjassa

- Loin t001-herrakoneella /srv/salt-hakemistoon uutta packages-tilamoduulia varten hakemiston komennolla ```sudo mkdir packages```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/80c918be-f3b4-4757-8ce6-9fe63261b9a6)

- Siirryin kyseiseen hakemistoon ja loin sinne tiedoston init.sls.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/94cd39e5-45fa-4b6d-87a1-b7a7cfbb415e)

- Loin tilamoduulin, jossa asennetaan cowsay- ja curl-ohjelmistopaketit, jos niitä ei ole entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6e7c63b3-3d6b-4773-b518-62579ff9a662)

- Seuraavaksi loin hakemistoon /srv/salt/hello top.sls-tiedoston, jossa määritetään tilamoduulien suorittaminen orjilla.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/28239c19-8b32-4b8d-a940-f05aace6b23d)

- Määritin aiemman kohdan a) hello-tilamoduulin ja packages-tilamoduulin suoritettavaksi kaikille orjille.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/7657b4c1-c87c-4fe7-a3a6-bf07254c3a5f)

- Suoritin t001-herrakoneella top.sls-tiedoston mukaiset tilamoduulit komennolla ```sudo salt '*' state.apply```. t002-orjakoneeseen laadittiin hellosls-tiedosto tmp-hakemistoon sekä ladattiin cowsay- ja curl-ohjelmistopaketit. Tässä tapauksessa top.sls-tiedoston osoittamat tilamoduulit suoritettiin vain t002-orjakoneessa, koska tämä kone on ainut orja t001-herrakoneelle.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/3910c8e0-0411-47b7-a52d-5ffc592afa3e)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/fb565db3-c4aa-4344-aa77-761b4c8cf719)

- Lopuksi tarkistin vielä t002-orjakoneella, että hellosls-tiedosto oli luotu tmp-hakemistoon sekä curl- ja cowsay-ohjelmistojen toiminnan.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/5d154829-4d34-487c-8f6c-6ce0f4f45551)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a2a3dd17-fd22-4339-9e43-8fd4193da81a)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/d637c6e7-a6ac-460e-baa3-103e0aebea88)

## c) Apache easy mode

### Apachen asentaminen käsin virtuaalikoneelle

- Asensin Apache2-ohjelmistopaketin t001-virtuaalikoneelle komennolla ```sudo apt-get install apache2```. Tarkistin Apachen toiminnan komennolla ```sudo systemctl status apache2```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/75f4921c-6065-4eed-8572-ad7064cc3828)

- Tarkistin Apache2-testisivun toiminnan komennolla ```curl -s localhost | grep title```. Kyseisellä komennolla saadaan näkyviin vain testisivun otsikko, eikä koko sivua.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/2bc23a2b-94d8-439a-ba58-cc77438ba4e4)

- Loin /home/vagrant-hakemistoon uuden webbi-hakemiston, johon puolestaan loin index.html-tiedoston Nano-tekstieditorilla. Kirjoitin index.html-tiedostoon vapaavalintaista tekstiä ilman ääkkösiä. Tästä tiedostosta tulee uusi Apachen etusivu testisivun tilalle.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a74c6091-5469-40a7-b220-8fc2a1e2d4de)

- Seuraavaksi siirryin Apachen konfiguraatiotiedostoihin (/etc/apache2). Täällä siirryin Apachen sites-available-hakemistoon, jonne loin uuden konfiguraatiotiedoston noora.conf Nano-tekstieditorilla. Käytin konfiguraatiotiedoston pohjana opettajan osoittamaa mallipohjaa, joka löytyy täältä: https://terokarvinen.com/2018/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Muutin pohjaan aiemmin luomani index.html-tiedoston sijainnin (/home/vagrant/webbi) DocumentRoot- ja Directory-kohtiin.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/0521b62b-98b7-46bd-b7de-9cea218e04ad)

- Tämän jälkeen siirryin /etc/apache2/sites-enabled-hakemistoon, joka sisältää symboliset linkit sites-available-hakemiston tiedostoihin. Poistin olemassa olevan linkin oletuskonfiguraatiotiedostoon (000-default.conf) komennolla ```sudo rm 000-default.conf```. Loin tilalle uuden symbolisen linkin uuteen konfiguraatiotiedostoon (noora.conf) komennolla ```sudo ln -s ../sites-available/noora.conf .```

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a9378e03-26ff-485e-971e-95afcfd2a0bc)

- Testasin toimivatko konfiguraatiot ja näkyykö uusi Apachen etusivu komennolla ```curl localhost | grep title```. Ei toiminut, vaan edelleen näkyi Apachen testisivu.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/3632eac1-a19e-4ec4-900e-3a8e8bab35c0)

- Apache2-palvelu tulee käynnistää uudelleen konfiguraatiotiedostoihin tehtyjen muutosten voimaan saattamiseksi. Käynnistin Apache2-palvelun uudelleen komennolla ```sudo systemctl restart apache2``` ja suoritin uudelleen komennon ```curl localhost | grep title```. Apachen testisivun sijasta tuli sivu, jonka otsikkona oli 403 Forbidden.
  
  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/57b47fd8-37ba-4b1d-a05e-27bee8137abf)

- Aloitin vianselvityksen, jonka tuloksena huomasin nopeasti, että olin tallentanut index.html-tiedoston /home/vagrant-hakemistoon enkä /home/vagrant/webbi-hakemistoon. Siirsin tiedoston haluttuun paikkaan komennolla ```mv index.html /home/vagrant/webbi/```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b3bd5325-e657-47b9-8385-7c897764a304)

- Käynnistin Apache2-palvelun taas uudelleen komennolla ```sudo systemctl restart apache2``` (jäi pois kuvasta). Tämän jälkeen suoritin myös uudelleen komennon ```curl localhost | grep title```, mutta taaskaan ei haluttua lopputulosta. Seuraavaksi suoritin komennon ```curl localhost``` ja luomani etusivun (index.html) otsikko tuli onnistuneesti näkyviin.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/01888665-95df-41c2-a322-7affc3c869d4)


## Lähteet

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 19.4.2024  

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (kohdat Infra as Code - Your wishes as a text file, top.sls - What Slave Runs What States). Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 19.4.2024.

Salt-ohjelmiston sisäinen manuaalisivu (sys.state_doc)

SaltProject 2024: Salt contributors – Salt overview (kohdat Rules of YAML, YAML simple structure, Lists and dictionaries – YAML block structures). Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml. Luettu 19.4.2024.




