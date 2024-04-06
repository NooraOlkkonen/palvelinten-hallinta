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

Loin virtuaalikoneille t001 ja t002 konfiguraatiotiedoston NotePad-tekstieditorilla. Käytin konfiguraatiotiedoston pohjana opettajan jakamaa konfiguraatiotiedostoa. Tallensin konfiguraatiotiedoston h2-hakemistoon.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a50ae087-867b-4b4e-ab57-754b36bb7822)

Konfiguraatiotiedoston nimessä näkyi tiedostopääte (.txt). Opin tiistain 2.4.2024 oppitunneilla, ettei konfugiraatiotiedosto toimi oikein, jos nimessä näkyy tiedostopääte. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/ebaf8551-c9cc-4016-9b70-96044b4a9beb)

Poistin tiedostopäätteen nimeämällä tiedoston uudelleen tiedostonhallinnassa. Järjestelmä varoitti tiedostopääteen poistamisesta.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/ac40aa7c-fa42-42af-a1e2-3cddfd8d2717)

Tämän jälkeen konfiguraatiotiedosto oli sellainen kuin pitää. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a3430fe3-a033-425f-bb98-7ddee535082c)

Käynnistin t001-virtuaalikoneen komennolla ```vagrant up t001```


## b) Salt herra-orja -arkkitehtuuri verkon yli



