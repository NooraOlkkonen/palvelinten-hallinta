# h1 Viisikko

Ensimmäisen viikon kotitehtävät. 

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävissä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

### Salt-komentojen suorittaminen paikallisesti

- Yleensä Salt-ohjelmistolla hallitaan yhtäaikaisesti suuria määriä tietokoneita.

- Salt-komentoja voi myös suorittaa paikallisesti. Tämä on hyödyllistä esim. harjoittelu- ja testausmielessä.

- Salt-komentojen suorittaminen paikallisesti tapahtuu lisäämällä komentoon parametrin --local.

- Tärkeimmät Salt-toiminnot ovat pkg, file, service, user ja cmd.

- Linux- ja Windows-käyttöjärjestelmissä toimii samat Salt-toiminnot.

### Verkkosivun luonti Githubin avulla

- Luodaan omaan Github-profiiliin uusi arkisto (create new repository).

- Arkiston luonnin yhteydessä määritetään arkiston tiedot ja asetukset: nimi, lyhyt kuvaus, julkisuus, lisenssi ja lisätään myös README-tiedosto.

- Luodaan arkistoon uusi tiedosto (add file - create new file) ja nimetään se. Oleellista on, että nimi on .md -loppuinen, jotta tiedosto muuntuu verkkosivuksi.

- Kirjoitetaan tiedostoon tekstiä MarkDown-merkintäkielellä ja tallennetaan muutokset (commit changes-painike).

### Raportin kirjoittaminen

- Raportti on kuvaus siitä mitä harjoituksessa on tehty ja tapahtunut.

- Raporttia tulee kirjoittaa samanaikaisesti harjoitusta tehdessä.

- Raportin tulee olla toistettava, täsmällinen ja helppolukuinen.

- Raporttiin tulee muistaa lisätä viittaukset lähteisiin, joita on käytetty harjoitusta tehdessä / raporttia laadittaessa.

- Sepittäminen, plagiointi ja kuvien luvaton kopiointi on kiellettyä.

## a) Hello Windows Salt Word!

Aloitin lataamalla tietokoneelle Salt-ohjelmiston Windows 64-bittiselle käyttöjärjestelmälle. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/fe5a345f-2369-4ceb-adaa-20ecca498603)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/4f7a3269-ab37-4e1b-8b9b-5202fc0a5f96)

Avasin Windows PowerShellin järjestelmänvalvojan oikeuksin. Selvitin Saltin asennuksen onnistumisen käyttämällä komentoa salt-call --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/bee571f7-6d8c-46ca-8f96-efdd5a70ae5c)

## b) Hello VirtualBox! / Hello Vagrant!

Latasin ensin tietokoneelle Oraclen VirtualBox-hypervisorin version 7.0.14 asennustiedoston. Ohjelman asennuksen yhteydessä tuli ilmoitukset Microsoft Visual C++ 2019 Redistributable Packagen lataamisesta, asennuksen ennenaikaisesta päättymisestä ja vakavasta virheestä asennuksen aikana. 

Googletin neuvoja ja asensin Microsoft Visual C++ 2019 Redistributable Packagen Youtube-videon ohjeiden avulla. Tämän jälkeen sain asennettua Virtual Boxin ilman ongelmia.
 
![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/469fe2bb-f3c9-4f21-9ff8-c7c3da1d84bb)

Seuraavaksi latasin Vagrant-ohjelman version 2.4.1 asennustiedoston. Tietokone tuli käynnistää uudelleen asennuksen jälkeen.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/0f610bff-55a7-41aa-9716-3a8a1288b0a0)

Avasin Windows PowerShellin järjestelmänvalvojan oikeuksin. Selvitin Vagrantin asennuksen onnistumisen käyttämällä komentoa vagrant --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/75a50317-c654-4edf-b2b0-b7d5551695a3)

## c) Linux-virtuaalikoneen luonti Vagrantilla

Loin oman kansion (bullseye) luotavalle virtuaalikoneelle. PowerShellissa siirryin kyseiseen kansioon ja suoritin komennon vagrant init debian/bullseye64. Seuraavaksi käynnistin virtuaalikoneen komennolla vagrant up, jolloin virtuaalikone käynnistyy VirtualBoxissa. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/788c04ac-62d4-46ba-bdf8-ee96e3104cbb)

Otin SSH-yhteyden virtuaalikoneeseen komennolla vagrant ssh.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e0aee916-0af1-4440-8cfd-a878967b0149)

## a) Salt-minionin asennus virtuaalikoneeseen

Latasin päivitykset virtuaalikoneeseen komennolla sudo apt-get update ja tämän jälkeen asensin Salt-ohjelmiston (salt-minion) komennolla sudo apt-get install salt-minion. Varmistuin Saltin asentumisesta komennolla sudo salt-call --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/2ce87f09-349a-4f06-b16f-2c1246a37857)

## b) Viisi tärkeintä

## c) Idempotentti

## d) Tietoja koneesta

## Lähteet

HashiCorp 2024: Install Vagrant. Luettavissa: https://developer.hashicorp.com/vagrant/install. Luettu 30.3.2024.

GameTrick 2022: Oracle VM VirtualBox Needs the Microsoft Visual C++ Redistributable Package Being Installed First. Katsottavissa: https://www.youtube.com/watch?v=xKTKgjUHu48. Katsottu 30.3.2024.

Karvinen 2023: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu: 29.3.2024.

Karvinen 2023: Create a Web Page Using Github. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/. Luettu: 29.3.2024.

Karvinen 2006: Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu 29.3.2024.

Oracle 2023: Download VirtualBox. Luettavissa: https://www.virtualbox.org/wiki/Downloads. Luettu 30.3.2024.

Salt Project 2024: Downloads. Luettavissa: https://docs.saltproject.io/salt/install-guide/en/latest/topics/downloads.html#windows. Luettu: 30.3.2024.


