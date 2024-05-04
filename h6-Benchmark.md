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
