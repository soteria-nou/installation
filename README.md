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

A) Ko uporabnik poda zahtevek po spletnih strani in če ta ne vsebuje IP naslova, DNS strežnik razvrsti uporabnikov zahtevek _glede na domeno_:

| pravilo | razlaga |
|---|---|
| `blk` | zahtevek se preusmeri na neobstoječi naslov (zahtevek se zavrže) |
| `hsn` | zahtevek ne sledi naslovu in se nadomesti s prazno vsebino |
| `hsr` | zahtevek sledi naslovu ali se nadomesti s prazno vsebino |
| `jun` | zahtevek ne sledi naslovu in se nadomesti s vsebino, ki zapre okno |
| `jur` | zahtevek sledi naslovu ali se nadomesti s vsebino, ki zapre okno |
| `rtl` | zahtevek se preusmeri na lokalni strežnik |
| `rtp` | zahtevek se preusmeri na lokalni posrednik |
| `rts` | zahtevek se preusmeri na zunanji strežnik |
| sicer | zahtevek se razreši v ustrezni IP naslov |

Če je zahtevek sledil naslovu, mora uporabnik ponovno podati zahtevek.

B) Na tem mestu je IP naslov že poznan in če zahtevek ni bil preusmerjen, požarni zid zavrne uporabnikov zahtevek _glede na IP naslov_, če je IP naslov na seznamu `blkip`, oziroma ga preusmeri na lokalni posrednik, če je IP naslov na seznamu `rtpip`.

C) Če je bil zahtevek preusmerjen na lokalni posrednik, posrednik zavrne uporabnikov zahtevek po spletni strani _glede na vsebino zahtevka_ po pravilih `action` ali obdela vrnjeno vsebino zahtevka glede na pravila `filter`. 

### Namestitev

Namestitev zahteva nekaj tehničnega znanja, a ni omejena na posebno strojno ali programsko opremo, vendar se priporoča programska oprema [Openwrt](https://openwrt.org/), kamor je potrebno namestiti zgoraj omenjeno programsko opremo.

Sistem lahko deluje v dveh načinih: neposredno in posredno. Prednost neposrednega načina je odsotnost kakršnega koli posega v naprave, na katerih želimo izboljšati uporabniško izkušnjo. Ta način je primeren ob velikem številu naprav.

#### Točka A (neposredno)

Najprej se potrebuje 8 IP naslovov, katere se pripne lokalni zanki. IP naslovi morajo biti prosti, zato je najbolje vzeti zasebne naslove (RFC 1918).
```
config interface 'soteria'
	option ifname 'lo'
	option proto 'static'
	list ipaddr '198.51.100.129'
	list ipaddr '198.51.100.130'
	list ipaddr '198.51.100.131'
	list ipaddr '198.51.100.132'
	list ipaddr '198.51.100.133'
	list ipaddr '198.51.100.134'
	list ipaddr '198.51.100.135'
	list ipaddr '198.51.100.136'
	option netmask '255.255.255.240'
```
Na te naslove se obesi storitve lokalnih strežnikov.

Za potrebe točke A) iz skice delovanje je potrebno datoteko `/etc/config/dhcp` dopolniti z
```
config dnsmasq
	list addnhosts '/tmp/dns'
```
To bo omogočilo programu _dnsmasq_ razvrščanje zahtevkov po domenah.

## Pomoč

Pomoč se izvaja preko [zahtevkov](https://github.com/soteria-nou/installation/issues).
