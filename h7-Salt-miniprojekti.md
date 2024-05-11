# h7 Salt-miniprojekti

[Palvelinten hallinta -opintojakson](https://terokarvinen.com/2024/configuration-management-2024-spring/) lopuksi toteutettu miniprojekti, jossa käytin opintojaksolla oppimiani tekniikoita.

## Miniprojektin tarkoitus

Usean virtuaalikoneen hallitseminen, hyödyllisten ohjelmistojen asentaminen hallittaviin koneisiin ja yhden ohjelmiston asetusten muuttaminen halutunlaisiksi. Edellä mainittujen toimien toteutus käyttämällä Salt-ohjelmiston herra-orja-arkkitehtuuria.

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

## Miniprojektissa tarvittavien virtuaalikoneiden luonti Vagrantilla

Loin tarvitsemani virtuaalikoneet Vagrant-ohjelmiston avulla ja hallitsin niitä Vagrantin kautta ssh-yhteydellä. Olin asentanut Vagrant-ohjelmiston fyysiseen tietokoneeseeni jo aiemmin opintojakson aikana.

Loin kolme virtuaalikonetta (n001, n002, n003). Käytin virtuaalikoneiden luonnissa pohjana opettaja Tero Karvisen [Vagrant-konfiguraatiotiedostoa](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant). Muokkasin konfiguraatiotiedostoa haluamaksi opettajan ja kurssikaveri [Saku Laitisen](https://github.com/KebabGarva) avustuksella niin, että n003-virtuaalikoneeseen asentuu myös graafinen käyttöliittymä.

Käyttämäni Vagrant-konfiguraatiotiedosto:

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/4df36cdb-54f9-408b-8622-81fd9ecaeb31)

Vagrant-konfiguraatiotiedoston määritykset eivät riittäneet graafisen käyttöliittymän saamiseksi n003-koneelle, vaan se tuli vielä erikseen asentaa komennolla ```sudo tasksel install xfce-desktop```. Jouduin myös vaihtamaan  vagrant-käyttäjän salasanan haluamakseni ssh-yhteyden kautta, jotta pääsin kirjautumaan koneelle graafisen käyttöliittymän kautta.

## Saltin herra-orja-arkkitehtuurin luonti

Loin Saltilla [herra-orja-arkkitehtuurin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant):

- herrakone (Salt-master): n001

- orjakoneet (Salt-minion): n002 + n003

Testasin herra-orja-arkkitehtuurin toimivuuden suorittamalla yksinkertaisen echo-komennon herralta orjakoneille:

![kuva](https://github.com/NooraOlkkonen/palvelinten-hallinta/assets/165004946/63f7918f-44c6-4cd4-98a5-79c0d9d26669)









