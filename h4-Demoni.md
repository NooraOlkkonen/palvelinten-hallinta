# h4 Demoni

Neljännen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävässä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

### 1. Karvinen 2023: Salt Vagrant – automatically provision one master and two slaves 

- **Infra as Code – Your wishes as a text file**

  - Luodaan hakemisto tilafunktio(i)lle, esim. moduuli hello &rarr; luodaan hakemisto /srv/salt/hello
  
  - Tähän hakemistoon luodaan init.sls-tiedosto, johon kirjoitetaan suoritettavaksi halutut tilafunktiot YAML-merkintäkielellä (infraa koodina)
  
  - hello-moduuli suoritetaan kaikille orjille komennolla ```sudo salt '*' state.apply hello```

 - **top.sls – What slave runs what states**

   - top.sls-tiedostoa käytetään määrittämään mitkä moduulit suoritetaan milläkin orjakonella
  
   - Hakemistoon /srv/salt/hello luodaan top.sls-tiedosto
  
   - Esim. jos hello-moduuli halutaan suorittaa kaikilla orjilla, top.sls-tiedostoon kirjoitetaan:

     ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e63d2abb-0cb9-46eb-bc5b-968d17cb4057)
  
   - Komennolla ```sudo salt '*' state.apply``` suoritetaan top.sls-tiedoston mukaiset moduulit

### 2. SaltProject 2024: Salt contributors – Salt overview 

- **Rules of YAML**

  - YAML-renderöijä on oletuksena monissa Saltin käyttämissä tiedostoissa: se kääntää YAML-tietorakenteen Python-tietorakenteeksi Saltin käyttöön
  
  - Tieto jäsennellään pareina (key: value)
  
  - Kirjainkoolla on merkitystä
  
  - Käytä välilyöntiä (ei tabulaattoria) sisennysten tekemiseen
  
  - Kommenteiksi tarkoitetut rivit aloitetaan #-merkillä

- **YAML simple structure**

  - YAML koostuu kolmesta peruselementistä: scalars, lists ja dictionaries
    
  - esim.

  ![image](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/abf7fea9-0793-4329-9e59-33850076b0d0)

- **Lists and dictionaries – YAML block structures**

  - YAML koostuu lohkorakenteista
  
  - Sisennys määrittää kontekstin
  
  - Kokoelmissa (lists & dictionaries) jokainen merkintä osoitetaan väliviivalla ja välilyönnillä ("- ")
 
### 3. Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port 

- Saltin avulla pystytään hallitsemaan useita demoneja 

- **package-file-service** -malli

  - ohjelman asentaminen (package, pkg)
    
  - konfiguraatiotiedoston korvaaminen (file)
    
  - demonin uudelleenkäynnistäminen (service) 

- SSH-palvelinportin muuttaminen Saltin avulla

  - luodaan herra-orja-arkkitehtuuri virtuaalikoneille 

  - luodaan herralle tilamoduuli (sshd.sls) 

  - luodaan herralle konfiguraatiotiedoston kopio (sshd_config), jossa muokataan SSH-porttinumeroa 

  - ajetaan tila kaikille orjille: ```sudo salt '*' state.apply sshd```
 
### 4. Salt tilafunktioiden ohjeet (Salt-ohjelmiston sisäinen manuaalisivu, sys.state_doc)

- **pkg**

  - johdanto: ohjelmistopakettien hallinta Saltilla

  - pkg.installed: varmistetaan, että nimetty ohjelmistopaketti on asennettu

  - pkg.purged: varmistetaan, että nimettyä ohjelmistopakettia ei ole asennettu 

  - pkgs: nimetään useampi ohjelmistopaketti toiminnon kohteeksi

- **file**

  - johdanto: toiminnot tiedostojen, hakemistojen ja symlinkkien hallitsemiseen / Saltilla voidaan manipuloida aggressiivisesti järjestelmän tiedostoja useilla eri tavoilla

  - file.managed: nimetyn tiedoston hallinta, esimerkiksi lataaminen herrasta orjaan 

  - file.absent: varmistaa, että nimetty tiedosto tai hakemisto puuttuu &rarr; jos tiedosto tai hakemisto on olemassa, se poistetaan 

  - file.symlink: luodaan symbolinen linkki haluttuun tiedostoon 

- **service**

  - johdanto: järjestelmään/palveluihin liittyvät ohjeet 

  - service.running: nimetyn palvelun toiminnan / käynnissäolon varmistaminen 

  - service.dead: varmistetaan, että tietty palvelu on pysäytetyssä tilassa / pysäytetään palvelu, mikäli se on toiminnassa

  - enable: nimetyn palvelun käyttöönotto käynnistyksen yhteydessä
 
## a) Hello SLS!

Tässä tehtävässä käytin aiemmassa h2-kotitehtävässä laatimaani virtuaalikonetta t001.

### Hei maailma -tila tekstitiedostona

- Loin hello-moduulia varten hakemiston komennolla ```sudo mkdir -p /srv/salt/hello```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/68922ad0-407d-49c6-b677-168d71294b6a)

- Siirryin kyseiseen hakemistoon ja loin sinne tiedoston init.sls.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e2995363-7afc-4091-b8ee-b1d57cf473bf)

- Loin tilamoduulin, jossa tmp-hakemistoon luodaan hellosls-niminen tiedosto, jos sitä ei ole entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1b6c8ada-7d33-4602-9646-02d3d4c9baf7)

- Suoritin hello-moodulin paikallisesti komennolla ```sudo salt-call --local state.apply hello```. /tmp/hellosls/-tiedosto luotiin onnistuneesti, koska sitä ei ollut entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6cf4b12b-17e7-4542-b7d7-9bc03e32306c)

- Tarkistin vielä tiedoston onnistuneen luonnin siirtymällä tmp-hakemistoon.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1c9eeafd-77f7-431c-bc0c-d43cbd09b40e)

## b) Top

Tässä tehtävässä käytin aiemmassa h2-kotitehtävässä laatimiani virtuaalikoneita t001 ja t002.

### Useiden moduulien/tilafunktioiden suorittaminen orjassa

- Loin t001-herrakoneella uuden hakemiston /srv/salt-hakemistoon packages-moduulia varten komennolla ```sudo mkdir packages```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/80c918be-f3b4-4757-8ce6-9fe63261b9a6)

- Siirryin kyseiseen hakemistoon ja loin sinne tiedoston init.sls.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/94cd39e5-45fa-4b6d-87a1-b7a7cfbb415e)

- Loin pkg.installed-tilafunktion, jossa asennetaan cowsay- ja curl-ohjelmistopaketit, jos niitä ei ole entuudestaan olemassa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6e7c63b3-3d6b-4773-b518-62579ff9a662)

- Seuraavaksi loin /srv/salt/hello/-hakemistoon top.sls-tiedoston, jossa määritetään moduulien suorittaminen orjilla.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/28239c19-8b32-4b8d-a940-f05aace6b23d)

- Määritin aiemman kohdan a) hello-moduulin ja packages-moduulin suoritettavaksi kaikille orjille.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/7657b4c1-c87c-4fe7-a3a6-bf07254c3a5f)

- Suoritin t001-herrakoneella top.sls-tiedoston mukaiset moduulit komennolla ```sudo salt '*' state.apply```. t002-orjakoneeseen laadittiin hellosls-tiedosto tmp-hakemistoon sekä ladattiin cowsay- ja curl-ohjelmistopaketit. Tässä tapauksessa top.sls-tiedoston osoittamat moduulit suoritettiin vain t002-orjakoneessa, koska tämä kone on ainut orja t001-herrakoneelle.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/3910c8e0-0411-47b7-a52d-5ffc592afa3e)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/fb565db3-c4aa-4344-aa77-761b4c8cf719)

- Lopuksi tarkistin vielä t002-orjakoneella, että hellosls-tiedosto oli luotu tmp-hakemistoon sekä curl- ja cowsay-ohjelmistojen toiminnan.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/5d154829-4d34-487c-8f6c-6ce0f4f45551)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a2a3dd17-fd22-4339-9e43-8fd4193da81a)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/d637c6e7-a6ac-460e-baa3-103e0aebea88)

## c) Apache easy mode

Tässä tehtävässä käytin aiemmassa h2-kotitehtävässä laatimiani virtuaalikoneita t001 ja t002.

### 1. Apachen asentaminen käsin virtuaalikoneelle

- Asensin Apache2-ohjelmistopaketin t001-virtuaalikoneelle komennolla ```sudo apt-get install apache2```. Tämän jälkeen tarkistin Apachen toiminnan komennolla ```sudo systemctl status apache2```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/75f4921c-6065-4eed-8572-ad7064cc3828)

- Tarkistin Apache2-oletussivun toiminnan komennolla ```curl -s localhost | grep title```. Kyseisellä komennolla saadaan näkyviin vain testisivun otsikko, eikä koko sivua.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/2bc23a2b-94d8-439a-ba58-cc77438ba4e4)

- Loin /home/vagrant/-hakemistoon uuden webbi-hakemiston, johon puolestaan loin index.html-tiedoston Nano-tekstieditorilla. Kirjoitin index.html-tiedostoon vapaavalintaista tekstiä ilman ääkkösiä. Tästä tiedostosta tulee uusi Apachen etusivu oletussivun tilalle.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a74c6091-5469-40a7-b220-8fc2a1e2d4de)

- Seuraavaksi siirryin Apachen konfiguraatiotiedostoihin (/etc/apache2/). Täällä siirryin Apachen sites-available-hakemistoon, jonne loin uuden konfiguraatiotiedoston noora.conf Nano-tekstieditorilla. Käytin konfiguraatiotiedoston pohjana opettajan osoittamaa mallipohjaa, joka löytyy täältä: https://terokarvinen.com/2018/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Muutin pohjaan aiemmin luomani index.html-tiedoston sijainnin (/home/vagrant/webbi/) DocumentRoot- ja Directory-kohtiin.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/0521b62b-98b7-46bd-b7de-9cea218e04ad)

- Tämän jälkeen siirryin /etc/apache2/sites-enabled/-hakemistoon, joka sisältää symboliset linkit sites-available-hakemiston tiedostoihin. Poistin olemassa olevan linkin oletuskonfiguraatiotiedostoon 000-default.conf komennolla ```sudo rm 000-default.conf```. Loin tilalle uuden symbolisen linkin uuteen konfiguraatiotiedostoon noora.conf komennolla ```sudo ln -s ../sites-available/noora.conf .```

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a9378e03-26ff-485e-971e-95afcfd2a0bc)

- Testasin toimivatko konfiguraatiot ja näkyykö Apachen uusi etusivu komennolla ```curl localhost | grep title```. Ei toiminut, vaan edelleen näkyi Apachen oletussivu.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/3632eac1-a19e-4ec4-900e-3a8e8bab35c0)

- Apache2-palvelu tulee käynnistää uudelleen konfiguraatiotiedostoihin tehtyjen muutosten voimaan saattamiseksi. Käynnistin Apache2-palvelun uudelleen komennolla ```sudo systemctl restart apache2``` ja suoritin uudelleen komennon ```curl localhost | grep title```. Apachen testisivun sijasta tuli sivu, jonka otsikkona oli 403 Forbidden.
  
  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/57b47fd8-37ba-4b1d-a05e-27bee8137abf)

- Aloitin vianselvityksen, jonka tuloksena huomasin nopeasti, että olin tallentanut index.html-tiedoston /home/vagrant/-hakemistoon enkä /home/vagrant/webbi/-hakemistoon. Siirsin tiedoston haluttuun paikkaan komennolla ```mv index.html /home/vagrant/webbi/```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b3bd5325-e657-47b9-8385-7c897764a304)

- Käynnistin Apache2-palvelun taas uudelleen komennolla ```sudo systemctl restart apache2``` (jäi pois kuvasta). Tämän jälkeen suoritin myös uudelleen komennon ```curl localhost | grep title```, mutta taaskaan ei haluttua lopputulosta. Seuraavaksi suoritin komennon ```curl localhost``` ja luomani etusivun (index.html) otsikko tuli onnistuneesti näkyviin.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/01888665-95df-41c2-a322-7affc3c869d4)

### 2. Apachen automaattinen asentaminen Saltilla

- Pysäytin käsin asentamani Apache2-ohjelman toiminnan t001-virtuaalikoneella komennolla ```sudo systemctl stop apache2```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e90f9dcc-699a-4bb2-86c4-a7619dd32c3f)

- Tämän jälkeen poistin Apachen komennolla ```sudo apt purge apache2```. Tämä komento poistaa Apache2-ohjelmiston sekä sen konfiguraatiotiedostot. Jouduin tosin poistamaan käsin /etc/apache2/sites-available-hakemiston ja noora.conf-tiedoston, koska niitä ei poistettu automaattisesti.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/7fd0738d-fec2-4e9b-98e0-6f1dd37a50f6)

- Tarkistin vielä Apache2-ohjelman statuksen ja varmistuin ohjelman onnistuneesta poistosta (unit apache2.service could not be found).

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/8af907c9-7338-4c8c-9a37-2bdf2ffc57e5)

- Loin jo olemassa olevaan /srv/salt/-hakemistoon apache-hakemiston, johon loin init.sls-tiedoston. Tein ensin testin file.managed-tilafunktion toimivuudesta.

   ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/378c4305-4db6-43ca-8395-78fc9c9d4cd5)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6bbea775-2ee6-498e-82c9-0834c1a4d15b)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/070dcea4-aeec-47d8-ad12-2e74fcf5ed97)

- Testin jälkeen aloin tekemään varsinaisia määrityksiä init.sls-tiedostoon Apache2-ohjelmistopakettia koskien. Määritin ensin Apache2-ohjelmistopaketin asennuksen pkg.installed-tilafunktiolla (**PKG**-file-service). Suoritin paikallisesti apache-moduulin komennolla ```sudo salt-call –local state.apply apache``` ja ohjelmistopaketin asennus onnistui.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/169bf4f2-8035-41e8-a9e4-381340e977c7)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/dcd8aa0c-ef87-4e9a-944f-f0959e495f7d)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/861a9bed-836d-4263-8f07-e05dcd8c244f)

- Loin jo olemassa olevaan /srv/salt/-hakemistoon etusivunoora-hakemiston, johon puolestaan loin index.html-tiedoston. Kirjoitin tiedostoon vapaamuotoista tekstiä, joka näkyy myöhemmin Apachen etusivuna. Kyseisenä hetkenä vielä näkyi Apachen oletusetusivu. 

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c68797f9-71ae-4a80-902d-81f8250c4d88)

- Seuraavaksi määritin init.sls-tiedostoon tilan Apache2-ohjelmiston käynnissäolosta service.running-tilafunktiolla (pkg-file-**SERVICE**).

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1445681d-ed87-498c-a83f-d51e869cfc1c)

- Suoritin uudelleen komennon ```sudo salt-call --local state.apply apache```. Ei tapahtunut muutoksia, koska Apache2-ohjelmisto on jo asennettu ja käynnissä.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e3b118ca-8097-40f3-8ccd-afc237d6ae0b)

 - Halusin vielä testata toimiiko Apachen asentaminen ja sen käynnissä olon varmistaminen Apache2-ohjelmiston poistamisen jälkeenkin. Ensin poistin Apache2-ohjelmiston komennolla ```sudo apt remove apache2``` (konfiguraatiotiedostot ei poistu) ja tämän jälkeen suoritin uudelleen komennon ```sudo salt-call --local state.apply apache```. Näytti toimivan.

   ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/90171cde-443c-45a9-b48a-2f9bc475054b)

- Loin konfiguraatiotiedoston noora.conf /etc/apache2/sites-available/-hakemistoon samalla tavalla kuin aiemmin Apachen käsin asentamisessa. noora.conf-tiedosto sisältää hakemistopolun aiemmin luotuun index.html-tiedostoon.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a31cdcce-350f-4851-9ec2-3b5ea657d44d)

- Kopioin noora.conf-tiedoston /srv/salt/apache/-hakemistoon komennolla ```sudo cp noora.conf /srv/salt/apache```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/38d6a76d-042b-4fe7-8124-395a977fa04a)

- Siirryin muokkaamaan init.sls-tiedostoa Apachen konfiguraatiotiedostojen suhteen (pkg-**FILE**-service). Käytin tässä tiistain 16.4.2024 opetuskerralla oppimiani määrityksiä:

  - konfiguraatiotiedostona toimii herrakoneen /srv/salt/apache/noora.conf/-tiedosto
 
  - luodaan symbolinen linkki /etc/apache/sites-available/noora.conf/-tiedostoon
 
  - symbolinen linkki 000-default.conf-tiedostoon on poissa

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/29b65556-eca0-4cde-8bcb-996917648d69)

- Testasin apache-moduulin toimivuuden suorittamalla paikallisesti komennon ```sudo salt-call --local state.apply apache```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/9760c5be-92d1-41f6-9ffd-298a01f91253)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a416f32b-67ef-47ca-82f9-a4b66de2a14a)

- Tarkistin komennolla ```curl -s localhost | grep title``` josko oman etusivuni teksti tulisi nyt näkyviin. Ei kuitenkaan tullut.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/61b82466-50b3-4ccd-aecf-e35d9bce130a)

- Yritin pohtia syytä tähän. Tarkastelin Apachen konfiguraatiotiedostojen hakemistoja. Jostain syystä symbolinen linkki noora.config-tiedoston oli punaisella. En keksinyt mikä tähän syynä tai miten tämä korjataan.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/5caa217b-61d3-417f-a1c8-cf0798455f74)

- Päätin aloittaa alusta. Poistin Apache2-ohjelmiston asennuksen ja käsin luomani tiedostot. Luin myös Apacheen liittyvää tehtäväraporttiani aikaisemmalta Linux-palvelimet -opintojaksolta. Raportin perusteella päätin kokeilla lähestymistapaa, jossa loin uuden etusivun (etusivu.html) /var/www/html/-hakemistoon. Otin varmuuskopion Apachen oletusetusivusta (index.html) ja muutin oman etusivu.html-tiedoston index.html-tiedostoksi.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/3179773e-32d5-4edb-b53a-95d77f018df2)

- Loin noora.conf-tiedoston /etc/apache2/sites-available/-hakemistoon. Merkitsin noora.conf-tiedostoon hakemistopolun index.html-tiedostoon.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/913c7d8d-d62d-4a3d-b966-accfc3cf28a5)

- Kopioin noora.conf-tiedoston /srv/salt/apache/-hakemistoon.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b73330fb-9508-4648-9a89-ae650e608b18)

- Muokkasin init.sls-tiedostoa. Jätin aiemmasta kokeilustani poiketen file.absent-tilafunktion pois. Tarkistin voiko sillä vaikutusta lopputulokseen.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/14b8402b-abb1-4420-8ce3-4fd94cb82726)

- Suoritin paikallisesti komennon ```sudo salt-call --local state.apply apache```, jonka tulokset kuvissa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b51623bc-c086-4c0a-9e1d-f8d081ffc747)

- Nyt symboliset linkit näyttivät oikealta ja oma etusivuni tuli näkyviin. Apache2-ohjelmiston asennus apache-moduulin konfiguraatioilla siis onnistui.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b1841a87-3af7-490d-9c69-a298e0bd0af5)

- Lisäsin kokeilumielessä vielä init.sls-tiedostoon file.absent-tilafunktion. Testasin vaikuttaako lopputulokseen.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/de0d586e-2796-46a9-9526-5f7dbdb8eaba)

- Suoritin uudelleen apache-moduulin ja tarkistin /etc/apache2/sites-enabled/-hakemiston sisällön. Symboliset linkit ok: 000-default.conf poissa, noora.conf sinisenä. Oma etusivu myös näkyi niin kuin pitää.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/f8aea5a4-719d-4917-9470-ab4adfd4a717)

- Jatkoin niin, että en suorittanutkaan enää apache-moduulia paikallisesti t001-herrakoneella, vaan suoritin moduulin kaikille orjille komennolla ```sudo salt '*' state.apply apache```. Tavoitteenani oli saada Apache2-ohjelmisto asentumaan ainoaan orjakoneeseen (t002). t002-koneen vastaus näytti ainakin lupaavalta.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/d10b47bc-1dc7-49fc-b884-5fe785e54610)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/feff715f-9767-4d91-aeef-4987cfe9aee7)

- Tarkistin Apache2-ohjelmiston statuksen t002-orjakoneella. Status oli aktiivinen, josta päätellen ohjelmisto asentui orjakoneeseen. 

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/586968d3-830d-4f56-82fb-1bfc00c41be4)

- Suoritin t002-orjakoneella komennon ```curl -s localhost | grep title``` tarkistaakseni Apachen etusivun. Näkyi Apachen oletussivu, eikä oma etusivuni. Tässä vaiheessa pää oli jo niin pyörällä, ettei ongelman ratkaisemiseen ollut enää energiaa.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/032a17e3-0628-404a-8100-ab4c6e267d11)

- Suoritin t002-orjakoneella vielä komennon ```curl 192.168.88.101``` (t001-herrakoneen IP-osoite on 192.168.88.101). Itse luomani Apache-etusivu näkyy t001-herralta t002-orjalle.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/bfb28b38-988d-4f46-9891-1d37557b1633)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b81d4597-750a-4eb1-bebc-356539ba4be3)

## d) SSHouto

Ajan puutteen vuoksi en valitettavasti ehtinyt perehtymään tehtävään ja tekemään sitä.

## Lähteet

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 19.4.2024  

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (kohdat Infra as Code - Your wishes as a text file, top.sls - What Slave Runs What States). Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 19.4.2024.

Lunkka-Salonen 2023: Linux-palvelimet -opintojakson (toteutus ICI003AS2A-3005, syksy 2023) luentodiat ja harjoitustehtävä Apache2-ohjelmistoon liittyen.

Salt-ohjelmiston sisäinen manuaalisivu (sys.state_doc)

SaltProject 2024: Salt contributors – Salt overview (kohdat Rules of YAML, YAML simple structure, Lists and dictionaries – YAML block structures). Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml. Luettu 19.4.2024.




