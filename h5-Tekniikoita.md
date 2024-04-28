# h5 Tekniikoita

Viidennen viikon kotitehtävät. 

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävissä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä 

Vapaavalintainen aiemman vuoden kotitehtäväraportti Saltin käytöstä Windowsilla

- Le Nguyen - [kotitehtävä 6: Windows](https://github.com/16cats/Infra-as-Code-course/blob/main/h6.md), Palvelinten hallinta -opintojakson syksyn 2023 toteutus
  
  - Windowsin asentaminen virtuaalikoneeseen (.iso-tiedoston lataaminen Microsoftin virallisilta sivuilta ja virtuaalikoneen luonti VirtualBoxilla)
    
  - Salt-ohjelmiston asentaminen Windows-virtuaalikoneeseen (asennukseen tarvittava ohjelmistopaketti ladataan Saltin virallisilta internetsivuilta)
    
  - Saltin toimivuuden testaaminen Windows PowerShellilla (Saltin ohjelmistoversion tarkistaminen)
    
  - Tietojen kerääminen Windows-koneesta komennolla grains.items
    
  - Saltin file.managed-tilafunktion testaaminen Windowsilla
    
  - Itselle uuden Salt-toiminnon kokeileminen Windowsilla

## a) Saltin asennus Windowsille

Asensin Salt-ohjelmiston käytössäni olevan fyysisen tietokoneen Windows 10 -käyttöjärjestelmään jo aiemmin ensimmäisessä kotitehtävässä h1 Viisikko. 

Avasin käytössäni olevalla fyysisellä tietokoneella Windows PowerShellin järjestelmänvalvojan oikeuksin. Tarkistin asennetun Saltin ohjelmistoversion komennolla ```salt-call --version``` ja varmistin Saltin käynnissäolon komennolla ```Get-Process salt*```. Testasin vielä Saltin toiminnan ajamalla paikallisesti user.present-tilafunktion komennolla ```salt-call --local state.single user.present omistaja```. Salt toimii, koska ei tullut virheilmoitusta ja komento antoi asianmukaisen vastauksen (omistaja-niminen käyttäjä on jo olemassa).

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/0a4a5b4b-5acc-4bac-9c8c-24bd006b2d41)

## b) Tietojen kerääminen Windows-koneesta Saltin avulla

Tutustuin käytössäni olevan fyysisen Windows-tietokoneen tietoihin käyttäen komentoa ```salt-call --local grains.items```. Valitsin muutamia keskeisiä tietoja, jotka sain eriteltyä näkyviin komennolla ```salt-call --local grains.item motherboard num_cpus osfullname saltpath```.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/0eec38b9-4ad4-4010-8248-b075f5460bdd)

- **motherboard** = emolevyn tiedot (tuotenimi ja sarjanumero)
  
- **num_cpus** = prosessorien lukumäärä
  
- **osfullname** = käyttöjärjestelmän koko nimi
  
- **saltpath** = Salt-ohjelmiston hakemistopolku

## c) Saltin file-tilafunktion testaaminen Windowsilla

Testasin Saltin file.managed-tilafunktiota siten, että C:/Windows/Temp/-hakemistoon luodaan tyhjä abc-niminen tiedosto, jos sitä ei ole siellä entuudestaan olemassa. Käytin tähän komentoa ```salt-call --local state.single file.managed C:/Windows/Temp/abc```. 

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/d73c93df-6d8b-4b9e-bc58-be7b03dc1642)

Idempotenssin testaamiseksi suoritin uudelleen paikallisesti saman komennon ```salt-call --local state.single file.managed C:/Windows/Temp/abc```. C:/Windows/Temp/-hakemistoon ei luotu uutta abc-nimistä tiedostoa, koska se oli jo olemassa.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/ac17b281-d6b3-439f-952f-4fbbbe58e70d)

Lopuksi varmistin vielä abc-tiedoston olemassaolon siirtymällä C:/Windows/Temp/-hakemistoon ja hain tiedoston näkyviin komennolla ```ls abc```.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/7c0bf4fb-88d2-4ed8-828c-e56aa0302cd8)

## d) CSI Kerava

Tein tämän tehtävän aiemmassa h2-kotitehtävässä luomallani Linux-virtuaalikoneella t001.

Hain viimeisimmäksi muokatut tiedostot /etc/-hakemistosta ja kotihakemistosta /home/vagrant/ komennolla ```find -printf '%T+%p\n' | sort```.

- ```find``` = tiedostojen etsiminen hakemistohierarkiasta

- ```-printf``` = print format = vakiomuotoinen tulostus

- ```%T``` = tiedoston viimeisin muokkausajankohta

- ```%p``` = tiedoston nimi

- ```\n``` = uuden rivin lisäys merkkijonon loppuun

- ```| sort``` = lajittelee tiedostot aikajärjestykseen

**/etc/-hakemiston viimeisimmäksi muokatut tiedostot:**

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/6b9b0eb7-cc8c-47c4-b19d-eb4acdd583d5)

**Kotihakemiston /home/vagrant/ viimeisimmäksi muokatut tiedostot:**

  ![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/dffa54b9-6ec6-4302-9891-dfe356edc75e)

## e) Komennus

Tehtävän tavoitteena oli tehdä Salt-tila, joka asentaa järjestelmään uuden komennon.

Aloitin uuden komennon lisäämisen luomalla /usr/local/bin/-hakemistoon uuden scripts-nimisen hakemiston. Loin tähän hakemistoon skripti.sh-tiedoston Nano-tekstieditorilla. skripti.sh-tiedostoon kirjoitin simppelin skriptin.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/456d4c50-fcac-47d9-9b61-f041b34d81e2)

Seuraavaksi muutin skripti.sh-tiedoston oikeuksia, jotta tiedosto voidaan suorittaa. Käytin komentoa ```sudo chmod ugo+x skripti.sh```, joka antaa tiedoston suoritusoikeudet tiedoston omistajalle, tiedoston ryhmään kuuluville käyttäjille sekä kaikille muille, jotka eivät kuulu äsken mainittuihin.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/44705831-0204-4a99-98e6-18d77915dd6c)

Suoritin skripti.sh-tiedoston komennolla ```./skripti.sh```, jolloin teksti "Sunnuntai-illan testailua" tuli näkyviin skriptin mukaisesti.

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/1094e3c1-3939-46ef-ab6f-8dbea2ddcac2)

Osaamiseni tämän tehtävän suhteen loppui tähän.

## Lähteet

Karvinen 2023: Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu: 27.4.2024.

Linux 2021: Find-komennon manuaalisivu. Luettu: 28.4.2024.

Lunkka-Salonen 2023: Linux-palvelimet -opintojakson (toteutus ICI003AS2A-3005, syksy 2023) luentodiat ja harjoitustehtävä Shell scripts-osioon liittyen. Luettu: 28.4.2024.

Microsoft 2024: Get-Process. Luettavissa: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-process?view=powershell-7.4. Luettu: 27.4.2024.

Nguyen 2023: Kotitehtävä 6 - Windows. Luettavissa: https://github.com/16cats/Infra-as-Code-course/blob/main/h6.md. Luettu: 27.4.2024.

Wikipedia 2021: chmod. Luettavissa: https://fi.wikipedia.org/wiki/Chmod. Luettu: 28.4.2024.




