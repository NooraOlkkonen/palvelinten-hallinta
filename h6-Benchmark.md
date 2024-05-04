# h6 Benchmark

Kuudennen viikon kotitehtävät. 

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävissä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

[Salt Project - Windows Package Manager ](https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html)

- **Introduction**

    - Salt mahdollistaa Linuxin kaltaisen paketinhallintatyökalun (ohjelmistopakettien asentamisen, päivittämisen, poistamisen ja hallinnan) myös Windows-käyttöjärjestelmälle
 
    - Paketinhallintatyökalu sisältää ohjelmistovaraston, joka puolestaan sisältää paketinmääritystiedostot
 
    - Paketinmääritystiedostot sisältävät kaikki tiedot, joita tarvitaan ohjelmiston asentamiseen Saltin avulla
 
    - Paketinmääritystiedostoja isännöidään Git-varastoissa ja oletusvarasto **salt-winrepo-ng** tulee kloonata Windows-käyttöjärjestelmään
 
    - Ohjelmistopakettien asentaminen tapahtuu **pkg.install**-funktiota käyttämällä
 
    - **pkg.installed**-funktiota käyttämällä voi tarkistaa onko tietty ohjelmistopaketti asennettu järjestelmään

- **Install libraries**

   - GitPython- tai pygit2-kirjaston asentaminen, jos Saltin Windows-paketinmääritystiedostoja isännöidään Saltin Git-varastossa (vapaaehtoinen)
   
- **Populate the local Git repository**

  - Oletusvaraston **salt-winrepo-ng** kloonaaminen Windows-käyttöjärjestelmään:

      -  Salt-herrassa komennolla: ```salt-run winrepo.update_git_repos```
 
      - herrattomassa Salt-minionissa komennolla: ```salt-call --local winrepo.update_git_repos```

- **Update minion database**

  - Paketinmääritystiedostoista luodaan tietokanta **pkg.refresh_db**-funktiolla:

      -  Salt-herrassa komennolla: ```salt -G 'os:windows' pkg.refresh_db```
 
      - herrattomassa Salt-minionissa komennolla: ```salt-call --local pkg.refresh_db```

- **Install software package**

    - Ohjelmistopakettien asentaminen tapahtuu **pkg.install**-funktion avulla:
 
      - Salt-herrassa komennolla: ```salt-call * pkg.install``` + 'ohjelmistopaketin nimi'
 
      - herrattomassa Salt-minionissa komennolla: ```salt-call --local pkg.install``` + "ohjelmistopaketin nimi"

- **Usage**

    - Yleisimpiä funktioita Windows-paketinhallintajärjestelmän käytössä:
 
      - **pkg.list_pkgs** (näyttää järjestelmään asennetut ohjelmistopaketit)
     
      - **pkg.list_available** (näyttää tietyn ohjelmistopaketin saatavilla olevat versiot)
     
      - **pkg.install** (asentaa määritetyn ohjelmistopaketin)
     
      - **pkg.remove** (poistaa määritetyn ohjelmistopaketin asennuksen)
     
## a) Paketti Windowsia

Ohjelmistopakettien asentaminen Windows-käyttöjärjestelmään Saltin avulla käyttämällä pkg.installed-funktiota. 

Tein tämän tehtävän jo tiistain 30.4.2024 opetuskerralla ja otin kuvakaappaukset tällöin. 

- Asensin Salt-minionin käytössäni olevaan fyysiseen Windows-tietokoneeseen jo aiemmin ensimmäisessä kotitehtävässä h1 Viisikko. Varmistin vielä Salt-minionin asennuksen komennolla ```Get-process salt*```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c301617f-155b-4eb9-9527-6ce4839a363f)

- Kloonasin Windows-paketinhallinnan oletusvaraston **salt-winrepo-ng** komennolla ```salt-call --local winrepo.update_git_repos```.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/296c4fa5-31d4-45ad-8f6c-adc200580122)

- Loin tietokannan paketinmääritystiedostoista komennolla ```salt-call --local pkg.refresh_db```. Yhteensä 312 paketinmääritystiedoston muuttaminen tietokannaksi onnistui.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/60f3527a-efa2-4d8d-9ee7-34e0c4971dcc)

- Kokeilin asentaa Cowsay- ja Curl-ohjelmistopaketit. Ei ilmeisesti onnistunut.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/c9fb517c-bea4-446d-970a-510d730ebcc2)

- Kokeilin seuraavaksi asentaa Putty-ohjelmistopaketin komennolla ```salt-call --local pkg.install "putty"```. Tämä näytti onnistuneen.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/ba3835dd-5d86-45d0-a4c6-81d266996866)

- Varmistin vielä Putty-ohjelmistopaketin asennuksen onnistumisen avaamalla itse ohjelman.

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6a015a54-35d7-46e3-a67c-34338fdbd587)





