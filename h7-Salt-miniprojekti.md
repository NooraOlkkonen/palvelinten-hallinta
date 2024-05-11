# h7 Salt-miniprojekti

[Palvelinten hallinta -opintojakson](https://terokarvinen.com/2024/configuration-management-2024-spring/) lopuksi toteutettu miniprojekti, jossa käytin opintojaksolla oppimiani tekniikoita.

## Miniprojektin tarkoitus

Usean virtuaalikoneen hallitseminen, hyödyllisten ohjelmistojen asentaminen hallittaviin koneisiin ja yhden ohjelmiston asetusten muuttaminen halutunlaisiksi. Edellä mainittujen toimien toteutus käyttämällä Salt-ohjelmiston herra-orja-arkkitehtuuria.

![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/150f3bb9-7f33-4df6-b099-0ce6150b7b54)

Projektissani loin edellä olevan kuvan mukaisen asetelman, jonka avulla tarkoituksenani oli havainnollistaa miten Saltin herra-orja-arkkitehtuuria käyttämällä voidaan hallita erityyppisiä tietokoneita. Käytin n002-konetta havainnollistamaan palvelintietokonetta ja n003-konetta puolestaan tavallista käyttäjätietokonetta, jossa on graafinen käyttöliittymä.

## Miniprojektissa käytetyt teknologiat

Fyysinen tietokone: VirtualBox versio 7.0.14, Vagrant versio 2.4.1

Virtuaalikoneet: käyttöjärjestelmä Debian 11 (Debian Bullseye64), Salt-master versio 3002.6, Salt-minion versio 3002.6 

## Miniprojektissa käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## Virtuaalikoneiden luonti Vagrantilla

Loin tarvitsemani virtuaalikoneet Vagrant-ohjelmiston avulla ja hallitsin niitä Vagrantin kautta ssh-yhteydellä. Olin asentanut Vagrant-ohjelmiston fyysiseen tietokoneeseeni jo aiemmin opintojakson aikana.

Loin kolme virtuaalikonetta (n001, n002, n003). Käytin virtuaalikoneiden luonnissa pohjana opettaja Tero Karvisen [Vagrant-konfiguraatiotiedostoa](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant). Muokkasin konfiguraatiotiedostoa haluamakseni opettajan ja kurssikaveri [Saku Laitisen](https://github.com/KebabGarva) avustuksella niin, että n003-virtuaalikoneeseen asentuu myös graafinen käyttöliittymä.

Käyttämäni Vagrant-konfiguraatiotiedosto:

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/4df36cdb-54f9-408b-8622-81fd9ecaeb31)

Vagrant-konfiguraatiotiedoston määritykset eivät riittäneet graafisen käyttöliittymän saamiseksi n003-koneelle, vaan se tuli vielä erikseen asentaa komennolla ```sudo tasksel install xfce-desktop```. Jouduin myös vaihtamaan vagrant-käyttäjän salasanan haluamakseni ssh-yhteydellä, jotta pääsin kirjautumaan koneelle graafisen käyttöliittymän kautta.

Poistin tässä vaiheessa n003-orjakoneelta Firefox-ohjelmiston, koska se oli asennettuna siihen valmiiksi. Ennen poistoa tarkistin komennolla ```dpkg -l | grep firefox``` mitä Firefox-paketteja koneessa oli. Varmistin ohjelmiston onnistuneen poiston suorittamalla saman komennon uudelleen poiston jälkeen. 

![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c9eb350d-2481-4d3f-a1e9-fe9ff527677f)

## Saltin herra-orja-arkkitehtuurin luonti

Loin Saltilla [herra-orja-arkkitehtuurin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant):

- herrakone (Salt-master): n001

- orjakoneet (Salt-minion): n002 + n003

Testasin herra-orja-arkkitehtuurin toimivuuden suorittamalla yksinkertaisen echo-komennon herralta orjakoneille:

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/63f7918f-44c6-4cd4-98a5-79c0d9d26669)

## Salt-moduulien luonti ohjelmistopakettien asentamista varten

Kahdelle virtuaalikoneelle asennetaan eri ohjelmistopaketit, joten tämän toteuttamiseksi tarvitsi luoda kaksi erilaista Salt-moduulia. Loin moduuleja varten n001-herrakoneelle /srv/salt/-hakemiston.

### 1. Salt-moduuli n002-orjakoneelle

- Loin n001-herrakoneen /srv/salt/-hakemistoon packages002-hakemiston.

- Loin packages002-hakemistoon init.sls-tiedoston, johon tein määritykset asennettavista Tree- ja Micro-ohjelmistopaketeista.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/72fb717d-489e-4f6c-830b-fa989249325f)

### 2. Salt-moduuli n003-orjakoneelle

- Loin n001-herrakoneen /srv/salt/-hakemistoon packages003-hakemiston.

- Loin packages003-hakemistoon init.sls-tiedoston, johon tein määritykset asennettavista Firefox- ja Gimp-ohjelmistopaketeista.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/e3361462-a5d0-4da7-a49d-98bcd724c669)

### 3. Salt-moduulien määrittäminen

- Loin n001-herrakoneen /srv/salt/-hakemistoon top.sls-tiedoston, jossa määritin mitkä moduulit suoritetaan milläkin orjakoneella:

  - n002-koneella packages002-moduuli
  
  - n003-koneella packages003-moduuli

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a8fa7060-fa91-4453-bb7a-571240452803)

## Salt-moduulien suorittaminen ohjelmistopakettien asentamiseksi

Suoritin n001-herrakoneella komennon ```sudo salt '*' state.apply```, jolloin top.sls-tiedostossa määritetyt moduulit suoritettiin orjakoneille.

- Firefoxin asentaminen epäonnistui n002-orjakoneeseen, eikä Gimpin asennuksesta tullut tietoja.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b8e585f6-06f7-41a7-b799-2a08497387a7)

- Micro asentui onnistuneesti n003-orjakoneeseen ja Tree olikin jo valmiiksi asennettuna.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1670c18c-3524-4176-8ff6-898533af5737)

Pohdin Firefoxin asennuksen ohjelmaa ja etsin neuvoja googlettamalla. Päädyin tarkistamaan apt-paketinhallinnasta saatavilla olevat Firefox-ohjelmistopaketit komennolla ```apt-cache pkgnames | grep firefox```. Huomasin, että saatavilla on firefox-esr-ohjelmistopaketti, jonka poistin aiemmin n003-koneesta. Muokkasin uudelleen n001-herrakoneen top.sls-tiedostoa, johon muutin asennettavaksi Firefox-paketiksi **firefox-esr**.

![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/87c225cb-a581-4f3b-8b82-69698bd35738)

Suoritin uudelleen n001-herrakoneella komennon ```sudo salt '*' state.apply```, jolloin:

- Micro- ja Tree-ohjelmistopaketit olivat jo asentuneet n003-orjakoneelle.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/325369e2-00e7-4331-ad1b-d72cf3a66286)

- Firefox-esr- ja Gimp-ohjelmistot asentuivat onnistuneesti n003-orjakoneelle.

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c3957268-0147-4d0d-a83c-c10baa8baad3)

Varmistin idempotenssin suorittamalla vielä kerran komennon ```sudo salt '*' state.apply```. Tuloksena kaikki määrittämäni ohjelmistopaketit oli jo asennettu orjakoneille, eikä muutoksia tehty.

![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1237df0c-4074-4b02-a85f-1a84533e2f47)

## Ohjelmistopakettien asentumisen varmistaminen

- n002-orjakoneen Micro- ja Tree-ohjelmistot:

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/2c513db8-473b-4ca5-a322-346c93e6f5b8)

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/a9833436-a87d-492d-85d7-dad3cfdbbba1)

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/51292c42-5ef3-4a65-8f12-39e2d4907b1f)

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/fa0de499-86db-445e-9312-b97a75a5a47c)

- n003-orjakoneen Firefox- ja Gimp-ohjelmistot, jotka avasin graafisen käyttäjäliittymän kautta:

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/f1e123ae-7879-43b3-b99b-0213aefe6d1c)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/be03fcb4-dcfa-4289-b65b-2139cb12727e)

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c6f515e2-a3c2-4b80-93b5-c071174625d5)

  ![image](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/4825add4-ffb4-46c8-aad2-212f8f7271cb)

## Firefox-selaimen aloitussivun määritys n003-orjakoneelle

Haaga-Helia ammattikorkeakoulun internetsivun (www.haaga-helia.fi) määrittäminen Firefox-selaimen aloitussivuksi n001-herrakoneelta n003-orjakoneelle. 

- Muutin ensin n003-orjakoneella selaimen aloitussivuksi Haaga-Helia ammattikorkeakoulun internetsivun itse Firefox-selaimen kautta.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/de3cb076-94a7-4f14-8b35-be9d956f4ff1)

- Etsin n003-orjakoneen kotihakemistosta viimeisimmäksi muokatut tiedostot komennolla ```find -printf "%T+ %p\n"|sort```. Näin pääsin käsiksi Firefoxin konfiguraatiotiedostoon **./.mozilla/firefox/mtzkiqmp.default-esr/prefs.js**:

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/f3a08f57-4d5f-4d77-a620-4bcd587e2de5)

- Löysin konfiguraatiotiedostosta tekemäni muutoksen aloitussivua koskien.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/2a19bd9b-3fb4-4ee8-9638-eb6dad90d1dd)

- Loin n001-herrakoneelle /srv/salt/packages003/-hakemistoon prefs.js-tiedoston, johon kopioin n003-koneen Firefox-konfiguraatiotiedoston sisällön. Sitten muokkasin packages003-moduulin init.sls-tiedostoa, niin että määritin n001-herrakoneen prefs.js-tiedoston siirtymään n003-orjakoneen Firefox-konfiguraatiotiedostoksi (file.managed-funktio).

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b72f42bd-b3a7-488f-af22-c8a39787df82)

- Poistin Firefox-ohjelmiston uudelleen n003-orjakoneelta ja suoritin n001-herrakoneella uudelleen ohjelmistopakettien asennusta varten laaditut moduulit komennolla ```sudo salt '*' state.apply```. Firefox-esr-ohjelmistopaketti asentui uudelleen ja konfiguraatiotiedosto päivittyi.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/4b20ff53-8c57-445c-b6a6-12e8a36d68db)

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/b3fc8fa1-1aca-49cd-82b2-c16e460b68a0)

- Idempotenssin toteamiseksi suoritin uudelleen komennon ```sudo salt '*' state.apply```, eikä muutoksia tehty.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/f0f2db7d-7e94-442f-8269-402ce2ac9e09)

- Avasin Firefox-selaimen n003-orjakoneella graafisen käyttöliittymän kautta, jolloin aloitussivuna avautui onnistuneesti Haaga-Helian internetsivu.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/de1b9318-c397-47d9-a433-4bde6461b47d)

## Lähteet: 

HashiCorp 2021: Virtualbox – Configuration. Luettavissa: https://developer.hashicorp.com/vagrant/docs/providers/virtualbox/configuration. Luettu: 7.5.2024. 

Hackreveal 2023: How to Uninstall and Reinstall Firefox in Ubuntu. Luettavissa: https://hackreveals.medium.com/how-to-uninstall-and-reinstall-firefox-in-ubuntu-3a27ed2fa968. Luettu: 8.5.2024. 

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 8.5.2024. 

Karvinen 2018: Two Machine Virtual Network with Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant. Luettu: 7.5.2024. 

Kunnari 2019: Salt mini-project. Luettavissa: https://irenekunnari.wordpress.com/salt-mini-project/. Luettu: 8.5.2024. 

Käyhkö 2019: Moduuliprojekti. Luettavissa: https://pakollinenlinuxblogi.wordpress.com/2019/05/15/moduuliprojekti/. Luettu: 8.5.2024. 

Shane 2018: Adding a GUI to a Debian Vagrant box. Luettavissa: https://shanemcd.org/2018/12/16/adding-a-gui-to-a-debian-vagrant-box/. Luettu: 7.5.2024. 

Tossavainen 2021: Oma moduli. Luettavissa: https://simotossavainen.wordpress.com/2021/05/19/h7-oma-moduli/. Luettu: 8.5.2024. 
