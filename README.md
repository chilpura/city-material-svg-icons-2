# 1. Grunticon
Grunticon on javascript-pohjainen tehtävien automatisoija, jota käytämme ikonien tuottamiseen Sähköisten palveluiden sivuja varten. Grunticonin etu on että sillä saadaan sekä korkealaatuiset svg-ikonit niitä svg:tä tukeviin selaimiin, että png-ikonit vanhempiin selaimiin joissa ei ole svg-tukea. Grunticon sisältää myös scriptin jolla selaimen ominaisuudet 'nuuskitaan' ja soveltuvat ikonit näytetään ominaisuuksien mukaan. Grunticonin käyttämiseen ei tarvita paljoakaan teknistä osaamista jos käytetään tekemääni pakettia sellaisenaan. Se mitä tarvitaan on muutamien ohjelmien asentaminen.

## 1.1 Tarvittavat ohjelmat
* [Node](https://nodejs.org/en/) 
* [Grunt](http://gruntjs.com)

# 2. Ikonikirjasto
Sähköisten palveluiden ikoni ja logoresurssien käyttö perustuu Grunticon-pohjaiseen automatisoijaan, jolla luodaan kuvaresurssit ja koodi kuvien käyttöönottamiseksi. Prosessi on seuraavanlainen: 

* Suunnittelija luo ikonin tai muun kuvan suunnitteluohjelmalla ja tallentaa sen .svg muodossa.
* Suunnittelija tai fronttikoodaaja ajaa kuvan Grunticon automatisoijan läpi, joka luo tarvittavan koodin ja kuvaresurssit.
* Kuvaresurssit ja koodi sijoitetaan kohdeympäristöön.

## 2.1. Suunnittelu 
Ikonien suunnitelussa ei ole mitään tavallisuudesta vektorikuvien luonnista poikkeavaa. Seuraavat asiat kannattaa kuitenkin ottaa huomioon. Eri värisistä ikoneista ei kannata tehdä duplikaatteja jos ainoa muuttuva asia on kuvan täyteväri. Grunticon pystyy luomaan eri värisiä versioita automaattisesti. (kts 2.). Toinen huomioitava asia on, että vektorielementtien ääriviiva (stroke) on aina oltava vektorin keskellä. Jotkin vektoriohjelmat mahdollistavat ääriviivan sijoittamisen viivan ulko tai sisäpuolelle, mutta svg-muoto ei tue tällaisia viivoja.

Svg-kuvat voi optimoida jollain työkalulla kuten [SVGOMG](https://jakearchibald.github.io/svgomg/), mutta se ei ole tarpeellista, koska Grunticon automatisoijassa on alatehtävä (svgmin) tätä varten. Halutessaan alatehtävän voi ohittaa kommentoimalla kyseisen tehtävän pois Gruntfile.js tiedostosta ja käyttää korvaavaa optimoijaa ennen Grunticonin käyttöä.

## 2.2. Grunticonin käyttäminen
Käsiteltävät kuvat sijoitetaan työkansioon  `svg_icons/raw` ja ajetaan komentoriviltä komento `$ grunt icons`. Lopputuloksena syntyvät hakemistot `compressed` ja `output` jos niitä ei aikaisemmin ollut olemassa. Kannattaa huomata että automatisoija poistaa kaikki olemassa olevat tiedostot kohdehakemistoista ja luo uudestaan kaikki kuvaresurssit joka kerta kun se ajetaan. `Output` hakemisto sisältää kaikki käyttöä varten tarvittavat tiedostot. `Compressed` hakemisto sisältää svgmin-nimisen alatehtävän tuottamat tilapäistiedostot. Grunticon tuottaa datauri-koodatut kuvat näistä tilapäistiedostoista. 

Grunticon luo `output` hakemistoon preview.html tiedoston, jota voi käyttää lopputuloksen tarkistamiseen selaimessa.

### 2.2.1. Väriversioiden tekeminen ikoneista
To be done.

## 2.3. Kuvaresurssien käyttö
Kaikki .css tiedostot (icons.data.png.css, icons.data.svg.css, icons.fallback.css) linkitetään projektiin ja grunticon.loader.js tiedoston sisältämä koodi lisätään html-sivun head elementtiin.