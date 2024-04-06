# h2 Soitto kotiin

Toisen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävissä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

Tiivistelmät opettajan osoittamista artikkeleista.

### Usean virtuaalikoneen luonti Vagrantin avulla

- Vagrant-ohjelmistolla voidaan hallita samanaikaisesti useita virtuaalikoneita VirtualBox-virtualisointialustalla. 

- Ladataan Vagrant-ohjelmisto fyysiseen isäntäkoneeseen.

- Luodaan fyysiseen isäntäkoneeseen oma hakemisto virtuaalikoneille ja luodaan siihen Vagrant-konfiguraatiotiedosto. Konfiguraatiotiedosto sisältää määritykset luotavia virtuaalikoneita koskien.

- Käynnistetään haluttu virtuaalikone: fyysisen isäntäkoneen komentokehotteessa annetaan komento ```vagrant up``` + virtuaalikoneen ID.

- Otetaan SSH-yhteys haluttuun virtuaalikoneeseen: fyysisen isäntäkoneen komentokehotteessa annetaan komento ```vagrant ssh``` + virtuaalikoneen ID.

### Salt Master ja Salt Slave


### Hello Salt Infra-as-Code

## a) Virtuaalikoneiden luonti ja niiden toimivuuden testaaminen

Asensin Vagrant-ohjelmiston fyysiseen tietokoneeseen edellisen kotitehtävän yhteydessä. Tarkistin asennetun Vagrant-ohjelmiston versio komennolla ```vagrant --version```

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6d25cb46-6ab8-4f37-b3d1-5042bbd0aee5)

Loin h2-nimisen hakemiston fyysiselle tietokoneelle tämän tehtävän virtuaalikoneita varten. Käytin hakemiston luontiin komentoa ```mkdir h2```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a9a77544-e169-44fe-9dcf-0461263a4942)

Loin virtuaalikoneille t001 ja t002 konfiguraatiotiedoston NotePad-tekstieditorilla. Käytin konfiguraatiotiedoston pohjana opettajan jakamaa konfiguraatiotiedostomallia. Tallensin konfiguraatiotiedoston h2-hakemistoon.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a50ae087-867b-4b4e-ab57-754b36bb7822)

Konfiguraatiotiedoston nimessä näkyi tiedostopääte (.txt). Opin tiistain 2.4.2024 oppitunneilla, ettei konfugiraatiotiedosto toimi, jos nimessä näkyy tiedostopääte. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/ebaf8551-c9cc-4016-9b70-96044b4a9beb)

Nimesin uudelleen konfiguraatiotiedoston ilman tiedostopäätettä .txt käyttämällä komentokehotteessa komentoa ```mv Vagrantfile.txt Vagrantfile```. Tämän jälkeen konfiguraatiotiedosto oli sellainen kuin pitää. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/c52b9ccc-e5ec-4b2b-80c3-ccdf6eecffdb)

Käynnistin t001-virtuaalikoneen komennolla ```vagrant up t001```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/02617b97-b28c-4b60-8a56-0ef0821fb795)

Otin SSH-yhteyden t001-virtuaalikoneeseen komennolla ```vagrant ssh t001```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/af477418-1b1c-4984-91ed-e11b9898b9d0)

Käynnistin myös t002-virtuaalikoneen ja otin siihenkin SSH-yhteyden.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/29e649c2-3ac5-4d4c-a409-3ed0ca363c1e)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/32775013-9115-4728-9519-846ac42d17a3)

Molemmat virtuaalitietokoneet näkyivät käynnistyneinä VirtualBoxissa.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/1afa27df-c32b-49cc-8c9c-5419716be28c)

Seuraavaksi tarkistin t001- ja t002-virtuaalikoneiden IPv4-osoitteet komennolla ```hostname -I```. Kyseisellä komennolla saadaan selville isäntänimen kaikkien verkkoliitäntöjen IPv4-osoitteet.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e5e546ef-7c89-4333-9b4e-5e21a9628af2)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/25201bb4-7e64-47b4-8c66-611ce7c8389f)

Testasin toimiiko yhteys t001- ja t002-virtuaalikoneiden välillä. Käytin tähän komentoa ```ping``` + virtuaalikoneen IPv4-osoite. Yhteys toimi kumpaankin suuntaan.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e662252c-1ae1-410d-a198-b6fd2377e74b)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/25d192fb-9495-4537-a776-ddd2b7419f2a)


## b) Salt herra-orja -arkkitehtuuri verkon yli


# Lähteet 

Karvinen 2023: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/. Luettu: 6.4.2024.

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 6.4.2024.

Karvinen 2023: Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/. Luettu: x.xx.xxxx.
 
Linux 2009: Hostname-komennon manuaalisivu. Luettu 6.4.2024.

