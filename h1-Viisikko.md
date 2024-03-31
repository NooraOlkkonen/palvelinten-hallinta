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

Tiivistelmät opettajan osoittamista artikkeleista.

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

- Kirjoitetaan tiedostoon tekstiä Markdown-merkintäkielellä ja tallennetaan muutokset (commit changes-painike).

### Raportin kirjoittaminen

- Raportti on kuvaus siitä mitä harjoituksessa on tehty ja tapahtunut.

- Raporttia tulee kirjoittaa samanaikaisesti harjoitusta tehdessä.

- Raportin tulee olla toistettava, täsmällinen ja helppolukuinen.

- Raporttiin tulee muistaa lisätä viittaukset lähteisiin, joita on käytetty harjoitusta tehdessä / raporttia laadittaessa.

- Sepittäminen, plagiointi ja kuvien luvaton kopiointi on kiellettyä.

## a) Hello Windows Salt Word!

Aloitin lataamalla Salt-ohjelmiston asennustiedoston käytössäni olevalle fyysiselle tietokoneelle ja suoritin asennuksen. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/fe5a345f-2369-4ceb-adaa-20ecca498603)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/4f7a3269-ab37-4e1b-8b9b-5202fc0a5f96)

Avasin Windows PowerShellin järjestelmänvalvojan oikeuksin. Selvitin Saltin asennuksen onnistumisen käyttämällä komentoa salt-call --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/bee571f7-6d8c-46ca-8f96-efdd5a70ae5c)

## b) Hello VirtualBox! / Hello Vagrant!

Latasin Oraclen VirtualBox-hypervisorin version 7.0.14 asennustiedoston käytössäni olevalle fyysiselle tietokoneelle. Asennuksen suorittamisen yhteydessä tuli ilmoitukset Microsoft Visual C++ 2019 Redistributable Packagen lataamisesta, VirtualBoxin asennuksen ennenaikaisesta päättymisestä ja vakavasta virheestä asennuksen aikana. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a220381e-6314-404d-b935-6f1d1324a6f2)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a7d782c7-9ff8-432f-ab85-077e81456d92)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/4c7d1f65-0100-48a8-bea0-86605e0826ad)

Googletin neuvoja ja asensin Microsoft Visual C++ 2019 Redistributable Packagen GameTrick-käyttäjän Youtube-videon ohjeiden avulla. Tämän jälkeen sain asennettua VirtualBoxin onnistuneesti.
 
![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/469fe2bb-f3c9-4f21-9ff8-c7c3da1d84bb)

Seuraavaksi latasin Vagrant-ohjelman version 2.4.1 asennustiedoston käytössäni olevalle fyysiselle tietokoneelle ja suoritin asennuksen. Tietokone tuli käynnistää uudelleen asennuksen jälkeen.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/0f610bff-55a7-41aa-9716-3a8a1288b0a0)

Tietokoneen uudelleen käynnistymisen jälkeen avasin Windows PowerShellin järjestelmänvalvojan oikeuksin. Selvitin Vagrantin asennuksen onnistumisen käyttämällä komentoa vagrant --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/75a50317-c654-4edf-b2b0-b7d5551695a3)

## c) Linux-virtuaalikoneen luonti Vagrantilla

Loin oman kansion (nimi: bullseye) käytössäni olevalle fyysiselle tietokoneelle virtuaalitietokonetta varten. PowerShellissa siirryin kyseiseen kansioon ja suoritin komennon vagrant init debian/bullseye64. Seuraavaksi käynnistin virtuaalikoneen komennolla vagrant up, jolloin virtuaalikone käynnistyi VirtualBoxissa. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/8a1f13ea-88f4-4b43-92e1-967519268a0d)

Otin etäyhteyden virtuaalikoneeseen SSH:ta käyttämällä (komento vagrant ssh).

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e0aee916-0af1-4440-8cfd-a878967b0149)

## d) Salt-minionin asennus virtuaalikoneeseen

Latasin päivitykset virtuaalikoneeseen komennolla sudo apt-get update ja tämän jälkeen asensin Salt-ohjelmiston (salt-minion) komennolla sudo apt-get install salt-minion. Varmistuin Saltin asentumisesta komennolla sudo salt-call --version.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/2ce87f09-349a-4f06-b16f-2c1246a37857)

## e) Viisi tärkeintä

Viiden tärkeimmän Salt-tilafunktion lyhyet esittelyt.

### 1. pkg

Ohjelmistopakettien hallitseminen (esim. määrittäminen asennettavaksi tai poistettavaksi).

Esimerkkinä määritin tree-nimisen paketin asennettavaksi komennolla sudo salt-call --local -l info state.single pkg.installed tree. Toiminto onnistui (succeeded: 1).

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/17485b09-415f-4219-a83a-c94070953998)

### 2. file

Tiedostojen hallitseminen. Tavallisia tiedostoja voidaan ladata master-koneesta ja sijoittaa kohdejärjestelmään käyttäen file.managed -tilaa.

Esimerkkinä määritin testitiedosto-nimisen tiedoston luotavaksi komennolla sudo salt-call --local -l info state.single file.managed /tmp/testitiedosto. Toiminto onnistui (Succeeded: 1).

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/df049bab-072a-46e3-8ade-1e3889139c54)

### 3. service

Palvelujen ja demonien käynnistämisen tai uudelleenkäynnistämisen määrittäminen.

Esimerkkinä määritin Apache2-palvelun käynnistämisen komennolla sudo salt-call --local -l info state.single service.running apache2 enable=True. Tämä kuitenkin epäonnistui (Result: False / Comment: The named service apacge 2 is not available / Failed: 1), koska Apache2-palvelua ei ole asennettu virtuaalikoneeseen. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/f37ae4b9-4dc5-40dc-be75-aeeb96798a9f)

### 4. user

Käyttäjäasetusten hallinta (esim. tietty käyttäjä tulee olla olemassa). 

Esimerkkinä määritin omistaja-nimisen käyttäjän olemassaolon komennolla sudo salt-call --local -l info state.single user.present omistaja. Käyttäjä luotiin, koska sitä ei ollut aiemmin olemassa (Comment: New user omistaja created). Toiminto onnistui (Succeeded: 1).

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6ccec7ab-2180-4c6a-ad4e-63f6558fd083)

### 5. cmd

Suoritettavien komentojen määrittäminen (esim. tietty komento suoritetaan, kun tietyt ehdot täyttyvät).

Esimerkkinä touch /tmp/foo -komennon suorittaminen. Käytin komentoa sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo". Toiminto onnistui (Succeeded: 1).

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/bf650d12-9787-43d2-8985-ce6767c5ece1)

## f) Idempotentti

Idempotentin toiminnon vaikutukset ovat samat toiminnon suorituskertojen lukumäärästä huolimatta. Esimerkiksi järjestelmään ei tule muutoksia, vaikka toiminto suoritettaisiin useampaan kertaan. Idempotentti toiminto voi myös olla toiminto, joka tekee muutoksen järjestelmään ensimmäisellä suorituskerralla, mutta ei saman toiminnon myöhemmillä suorituskerroilla. Saltin tilafunktioiden tulisi olla idempotentteja.

Valitsin esimerkiksi idempotentistä toiminnosta Saltin user-tilafunktion. Aiemmin tehtävässä e) loin omistaja-nimisen käyttäjän. Kun suoritin uudelleen komennon ```sudo salt-call --local -l info state.single user.present omistaja```, toista samannimistä käyttäjää ei enää luotu. Sen sijaan tuli ilmoitus kyseisen käyttäjän olemassaolosta (Comment: User omistaja is present and up to date). Siis kun sama komento suoritettiin uudelleen, mitään muutoksia ei tehty.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/db741ed4-c5a7-4ec3-ae1f-925349ff4ce6)

## g) Tietoja koneesta

Tutustuin virtuaalikoneen tietoihin käyttäen komentoa ```sudo salt-call --local grains.items```. Poimin kolme mielenkiintoista tietoa, jotka sain eriteltyä komennolla ```sudo salt-call --local grains.item osfinger shell saltversion```. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/16ee485b-c9b6-4bf6-a2be-eb8d150d6df6)

- osfinger = kertoo virtuaalikoneen käyttöjärjestelmän

- saltversion = kertoo virtuaalikoneeseen asennetun Salt-ohjelmiston version

- shell = kertoo virtuaalikoneen komentotulkin

## Lähteet

HashiCorp 2024: Install Vagrant. Luettavissa: https://developer.hashicorp.com/vagrant/install. Luettu 30.3.2024.

GameTrick 2022: Oracle VM VirtualBox Needs the Microsoft Visual C++ Redistributable Package Being Installed First. Katsottavissa: https://www.youtube.com/watch?v=xKTKgjUHu48. Katsottu 30.3.2024.

Karvinen 2023: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu: 29.3.2024.

Karvinen 2023: Create a Web Page Using Github. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/. Luettu: 29.3.2024.

Karvinen 2006: Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu 29.3.2024.

Oracle 2023: Download VirtualBox. Luettavissa: https://www.virtualbox.org/wiki/Downloads. Luettu 30.3.2024.

Salt Project 2024: Downloads. Luettavissa: https://docs.saltproject.io/salt/install-guide/en/latest/topics/downloads.html#windows. Luettu: 30.3.2024.

Salt Project 2024: Glossary - Idempotent. Luettavissa: https://docs.saltproject.io/en/latest/glossary.html. Luettu 31.3.2024.

Salt Project 2024: Salt.states.pkg. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg.html. Luettu 31.3.2024.

Salt Project 2024: Salt.states.file. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html. Luettu 31.3.2024.

Salt Project 2024: Salt.states.service. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.service.html. Luettu 31.3.2024.

Salt Project 2024: Salt.states.user. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.user.html. Luettu 31.3.2024.

Salt Project 2024: Salt.states.cmd. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cmd.html. Luettu 31.3.2024.

Wikipedia 2019: Idempotenssi. Luettavissa: https://fi.wikipedia.org/wiki/Idempotenssi. Luettu: 31.3.2024.
