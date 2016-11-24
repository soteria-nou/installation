Do nadaljnjega bo vse znanje zbrano na tej strani.

# Soteria nou

## Ideja

Ideja je izboljšati uporabnikovo izkušnjo pri uporabi svetovnega spleta (2.0 in naprej).

Spletna izkušnja bo boljša:
* če bo prikaz spletnih strani hitrejši,
* če bo možnost okužb z zlonamerno programsko kodo nižja,
* če bo zmožnost prepoznavanja navad in običajev uporabnika omejena,
* če se vsebina, katere uporabnik ni zahteval, ne bo prikazovala ali se mu ne bo vsiljevala, in
* če bo spletna stran ohranila svoj prvoten namen.

Neprestana težnja k takšnemu izboljšanju pomeni, da to ni nekaj, kar se naredi enkrat in bo tako večno ostalo. Potreben je nenehni razvoj, ki bo sledil predstavljeni ideji in smernicam.

Izvedba mora biti uporabniku prijazna.

## Izvedba

Trenutno izvedbo sestavljajo pravila, ki nastavljajo požarni zid, strežnik za DNS in HTTP posrednika. Programska oprema in pravila so javno dostopna in tako omogočajo vpogled v delovanje. V nasprotju z uveljavljenimi rešitvami, kot so adblock razširitve za brskalnik, takšna zasnova omogoča razvrščanje uporabnikovih zahtevkov še predenj ti dosežejo spletno mesto, kar zmanjša količino poslanih in prejetih podatkov.

Uporabljena programska oprema:
* [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html)
* [privoxy](https://www.privoxy.org/)
* [tinysrv](https://github.com/jaka/tinysrv/)

### Namestitev

Namestitev zahteva nekaj tehničnega znanja.

## Pomoč

Pomoč se izvaja preko [zahtevkov](https://github.com/soteria-nou/installation/issues).

