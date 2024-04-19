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

## Lähteet

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 19.4.2024  

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (kohdat Infra as Code - Your wishes as a text file, top.sls - What Slave Runs What States). Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 19.4.2024.

Salt-ohjelmiston sisäinen manuaalisivu (sys.state_doc)

SaltProject 2024: Salt contributors – Salt overview (kohdat Rules of YAML, YAML simple structure, Lists and dictionaries – YAML block structures). Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml. Luettu 19.4.2024.




