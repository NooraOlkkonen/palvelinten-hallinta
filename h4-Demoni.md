# h4 Demoni

Neljännen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## x) Lue ja tiivistä

### 1. Karvinen 2023: Salt Vagrant – automatically provision one master and two slaves 

- Infra as Code – Your wishes as a text file

  - Luodaan hakemisto tilamoduulille, esim. moduuli hello -> luodaan hakemisto /srv/salt/hello
  
  - Tähän hakemistoon luodaan init.sls-tiedosto, johon kirjoitetaan suoritettavaksi halutut toiminnot YAML-merkintäkielellä (infraa koodina)
  
  - hello-moduuli suoritetaan kaikille orjille komennolla sudo salt ’*’ state.apply hello

 - top.sls – What slave runs what states

   - top.sls-tiedostoa käytetään määrittämään mitkä moduulit suoritetaan milläkin orjakonella
  
   - Hakemistoon /srv/salt/hello luodaan top.sls-tiedosto
  
   - Esim. jos halutaan suorittaa hello-moduuli kaikilla orjilla, top.sls-tiedostoon kirjoitetaan base: ’*’: -hello
  
   - Komennolla sudo salt ’*’ state.apply suoritetaan top.sls-tiedoston mukaiset moduulit

### 2. SaltProject 2024: Salt contributors – Salt overview 

- Rules of YAML

  - YAML-renderöijä on oletuksena monissa Saltin käyttämissä tiedostoissa: se kääntää YAML-tietorakenteen Python-tietorakenteeksi Saltin käyttöön
  
  - Tieto jäsennellään pareina (key: value)
  
  - Kirjainkoolla on merkitystä
  
  - Käytä välilyöntiä (ei tabulaattoria) sisennysten tekemiseen
  
  - Kommenteiksi tarkoitetut rivit aloitetaan #-merkillä

- YAML simple structure

  - YAML koostuu kolmesta peruselementistä: scalars, lists ja dictionaries

  ![image](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/abf7fea9-0793-4329-9e59-33850076b0d0)

- Lists and dictionaries – YAML block structures

  - YAML koostuu lohkorakenteista
  
  - Sisennys määrittää kontekstin
  
  - Kokoelmissa (lists & dictionaries) jokainen merkintä osoitetaan väliviivalla ja välilyönnillä (”- ”)

## Lähteet

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (kohdat Infra as Code - Your wishes as a text file, top.sls - What Slave Runs What States). Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 19.4.2024.

SaltProject 2024: Salt contributors – Salt overview (kohdat Rules of YAML, YAML simple structure, Lists and dictionaries – YAML block structures). Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml. Luettu 19.4.2024.




