# h3 Toimiva versio

Kolmannen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävässä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

### 1. Getting Started - What is Git? (Chacon and Straub 2014)

- Git käsittää datan ja käsittelee sitä eri tavalla kuin muut versionhallintajärjestelmät -> Gitissä data nähdään tilannekuvien virtana.

- Gitissä monia toimintoja pystyy suorittamaan käyttämällä pelkästään paikallisia resursseja ilman internetyhteyttä.

- Melkein kaikki Gitin toiminnot vain lisäävät dataa Gitin tietokantaan.

- Tiedostojen päätilat Gitissä:
  
    - modified = tiedostoon on tehty muutoksia, mutta sitä ei ole tallennettu tietokantaan
      
    - staged = muokattu tiedosto on merkitty menemään tallennettavaan tilannekuvaan (commit snapshot)
      
    - committed = data on tallennettu paikalliseen tietokantaan

### 2. Komento: git add . && git commit; git pull && git push

- git add . = git add --all = valitaan kaikki varaston tiedostot git commitia varten

- git commit = tallentaa varastoon tehdyt muutokset, eli laatii ns. tilannekuvan (snapshot) varastosta

- git pull = päivittää etänä tehdyt muutokset paikalliseen varastoon

- git push = paikallisesti tehdyt muutokset päivitetään/julkaistaan etävarastoon

## a) Online

- Loin webliittymän kautta Githubiin uuden varaston (repository), jonka nimestä ja kuvauksesta löytyy sana "summer". Loin varastoon myös tiedoston (README.md) ja lisenssin (GNU General Public Licence 3).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e5d5c84a-307d-4279-a214-f8dda294e6b2)

## b) Dolly

- Kloonasin kohdassa a) luomani varaston fyysiselle tietokoneelle aiemmin luomaani git-hakemistoon. Kloonaaminen tapahtui fyysisen tietokoneen komentokehotteessa komennolla ```git clone``` + varaston SSH-linkki. Sain varaston SSH-linkin Githubin webliittymästä varaston tiedoista (code-kohta).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/109ad78a-11c3-4953-8d74-8d66ed33d954)

- Loin varastoon uuden tiedoston (plan-a.md) NotePad-tekstieditorilla komentokehotteen kautta.
  
  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/aa52499f-456e-4296-9456-84460f5f9803)

- Suoritin komennon ```git add .```

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6c4fa3a1-2f2d-47b1-b96a-6e80057d801e)

- Suoritin komennon ```git commit```, jolloin järjestelmä huomautti tekijän tuntemattomasta henkilöllisyydestä.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/2846a171-1975-48a0-881d-b98c541389c6)

- Päivitin tekijän henkilöllisyyden seuraavilla komennoilla: ```git config --global user.email``` ja ```git config --global user.name``` 

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/1613d890-9c4e-4e85-ac7e-645ce37ebf64)

- Suoritin komennon ```git pull```

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/791e7459-0521-4e61-9e70-812dc94e6b94)

- Suoritin komennon ```git push```

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/4f602b53-cc34-4c6e-bb8c-b1ace5372be2)

- Muutos (plan-a.md-tiedoston lisääminen varastoon) ei päivittynyt Githubin webbiliittymään.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/5d2a4e6b-18df-4b61-a923-a60d2af57a66)

- Loin varastoon uuden tiedoston (plan-b.md) NotePad-tekstieditorilla komentokehotteen kautta.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/86092810-816f-4123-bca5-577bfda2e377)

- Suoritin uudelleen komennot ```git add .``` + ```git commit``` + ```git pull``` + ```git push```. Komennon ```git commit``` yhteydessä kirjoitin commit messagen, eli selityksen tehdyistä muutoksista (Add plan-b.md file).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/7edf38ab-55dc-4baa-b116-8130e7a70d44)

- Fyysisen tietokoneen komentokehotteen kautta luomani tiedostot (plan-a.md, plan-b.md) päivittyivät myös Githubin webbiliittymään.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/f70e5688-2fc6-4cb1-8951-43fb27b5acf8)

### Huomioita tehtävästä:

- Tiistain 9.4.2024 opetuskerralla huomasin, ettei komento ```git add . && git commit; git pull && git push``` toimi sellaisenaan Windows-käyttöjärjestelmän komentokehotteessa. Komennon osat voi suorittaa Windowsilla yksittäisinä, kuten tein tässä tehtävässä.

- Komennot ```git add .``` + ```git commit``` + ```git pull``` + ```git push``` olisi pitänyt suorittaa heti varaston kloonaamisen jälkeen ennen tiedoston plan-a.md luontia varastoon. Olisin myös voinut jättää uuden tiedoston plan-b.md tekemättä ja vain suorittaa uudelleen komennot ```git add .``` + ```git commit``` + ```git pull``` + ```git push```, jolloin tiedosto plan-a.md olisi päivittynyt Githubin webbiliittymään. Kun suoritin komennot ```git add .``` + ```git commit``` + ```git pull``` + ```git push``` tiedoston plan-b.md laatimisen jälkeen, päivittyivät molemmat tiedostot (plan-a.md ja plan-b.md) samalla kertaa Githubin webbiliittymään.

## c) Doh!

## d) Tukki

## e) Suolattu rakki

## Lähteet

Git Guides 2024a. Git Add. Luettavissa: https://github.com/git-guides/git-add. Luettu: 14.4.2024.

Git Guides 2024b. Git Commit. Luettavissa: https://github.com/git-guides/git-commit. Luettu: 14.4.2024.

Git Guides 2024c. Git Pull. Luettavissa: https://github.com/git-guides/git-pull. Luettu: 14.4.2024.

Git Guides 2024d. Git Push. Luettavissa: https://github.com/git-guides/git-push. Luettu: 14.4.2024.

