Do nadaljnjega bo vse znanje zbrano na tej strani.

# Soteria nou

## Ideja

Ideja je izboljšati uporabnikovo izkušnjo pri uporabi svetovnega spleta (2.0 in naprej).

Spletna izkušnja bo boljša:
* če bo prikaz spletnih strani hitrejši,
* če bo možnost okužb z zlonamerno programsko kodo nižja,
* če bo zmožnost prepoznavanja navad in običajev uporabnika omejena,
* če se vsebina, katere uporabnik ni zahteval, ne bo prikazovala ali se mu ne bo vsiljevala, in
* če bo spletna stran ohranila svoj prvotni namen.

Neprestana težnja k takšnemu izboljšanju pomeni, da to ni nekaj, kar se naredi enkrat in bo tako večno ostalo. Potreben je nenehni razvoj, ki bo sledil predstavljeni ideji in smernicam.

Izvedba mora biti uporabniku prijazna.

## Izvedba

Trenutno izvedbo sestavljajo pravila, ki nastavljajo požarni zid, strežnik za DNS in HTTP posrednika. Programska oprema in pravila so javno dostopna in tako omogočajo neprikrit vpogled v delovanje, s čimer se lahko ovrednoti začrtane smernice. V nasprotju z uveljavljenimi rešitvami, kot so razne razširitve za brskalnik, takšna zasnova omogoča razvrščanje uporabnikovih zahtevkov v lokalnem omrežju še preden ti dosežejo spletno mesto, kar zmanjša količino poslanih in prejetih podatkov.

Uporabljena programska oprema:
* [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html)
* [privoxy](https://www.privoxy.org/)
* [tinysrv](https://github.com/jaka/tinysrv/)

#### Skica delovanja

Strežnik DNS razvrsti uporabnikov zahtevek _glede na domeno_:

| pravilo | razlaga |
|---|---|
| `blk` | zahtevek se preusmeri na neobstoječi naslov |
| `hsn` | zahtevek ne sledi naslovu in se nadomesti s prazno vsebino |
| `hsr` | zahtevek sledi naslovu ali se nadomesti s prazno vsebino |
| `jun` | zahtevek ne sledi naslovu in se nadomesti s vsebino, ki zapre okno |
| `jur` | zahtevek sledi naslovu ali se nadomesti s vsebino, ki zapre okno |
| `rtl` | zahtevek se preusmeri na lokalni strežnik |
| `rtp` | zahtevek se preusmeri na lokalni posrednik |
| `rts` | zahtevek se preusmeri na zunanji strežnik |
| sicer | zahtevek se razreši v ustrezni naslov |

Požarni zid zavrne uporabnikov zahtevek _glede na IP naslov_, če je IP naslov na seznamu `blkip`, oziroma ga preusmeri na lokalni posrednik (pravilo `rtpip`).

Lokalni posrednik zavrne uporabnikov zahtevek po spletni strani _glede na vsebino_ glede na pravila seznama `action` ali obdela vrnjeno vsebino glede na pravila `filter`.

### Namestitev

Namestitev zahteva nekaj tehničnega znanja.

## Pomoč

Pomoč se izvaja preko [zahtevkov](https://github.com/soteria-nou/installation/issues).

