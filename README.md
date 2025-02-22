# Analiza animejev
Analiziral bom vseh (okrog 13000) uvrščenih animejev na strani [MyAnimeList](https://myanimelist.net/).  
  
Za vsak anime bom zajel:
* naslov
* opis
* način predvajanja (TV, Film, Internet, Video)
* število epizod
* status (končan, še poteka, še ni potekal)
* začetek predvajanja
* konec predvajanja
* producente
* studije
* vir (manga, lahki roman, spletna manga, originalno delo)
* žanre
* dolžino posamezne epizode
* starostno oceno (PG-13, R-17+)
* povprečno oceno vseh uporabnikov
* rank (neka uvrstitev odvisna od ocene in popularnost, izračunana z MAL algoritmom)
* popularnost (uvrstitev glede na druge animeje)
* število uporabnikov (, ki si bodisi je ali namerava ta anime ogledat)
* favoriti (koliko uporabnikov je označilo ta anime kot eden svojih najljubših)

Delovne hipoteze:
* S popularnostjo se povprečna ocena viša, do neke meje, od kjer naprej začne padati.
* Animeji predvajani na televiziji so bolj popularni od tistih z drugih virov.
* Animeji z starostno oceno R-17+ so povprečno bolje ocenjeni od drugih.
* Comedy je najslabše ocenjen žanr, a pri tem najbolj popularen.
* S številom žanrov se popularnost animeja veča.
* Povprečna ocena vseh filmov je nižja kot tista vseh animejev (predvajanih po televiziji).
* Povprečna ocena vseh animejev se z leti veča.
* Povprečna ocena se z dolžino animeja manjša, a popularnost veča, prav tako kot število favoritov.
* Z količino animejev, ki jih studio izdela se njihova povprečna popularnost veča.

## Priprava podatkov
Podatke sem zajel s strani [Top Anime - MyAnimeList.net](https://myanimelist.net/topanime.php) s skripto [download.py](download.py), ki prenese prvih x strani. Nažalost je na top listu vidno manj podatkov kot sem si želel, zato nasledenj del skripte zajame in zapiše zgolj linke do podrobnejših opisov posameznega animeja. Nato pa prenese še vse strani na teh linkih.  
  
Pojavila se je težava, da mi je prejšnja skripta začela prenašati neveljavne strani (npr. Too many requests, Page not found). Zato je tu [unlucky.py](unlucky.py), ki pobriše neveljavne strani, to pa dela kasneje še deloma [edit.py](edit.py).  
  
Skripta [edit.py](edit.py) zajame podatke za posamezen anime ki so napisani čisto na vrhu. Te podatke očisti in ustvari [anime.json](data/anime.json), ter naslednje csv-je:
* [anime.csv](data/anime.csv), ki vsebuje večino podatkov o animejih prav tako pa njihove id-je
* [genres.csv](data/genres.csv) in [producers.csv](data/producers.csv), ki vsebujej podatke o žanrih in njihove id-je, ter podatke o producentih oz. studijih ter njihov id-je
* [linkedgenres.csv](data/linkedgenres.csv), [linkedproducers.csv](data/linkedproducers.csv) in [linkedstudios.csv](data/linkedstudios.csv) ki vsebujejo povezave med animeji ter žanri, producenti ter studiji respektivno. Lahko bi združil slednji dve tabeli ter dodal še stolpec "vloge", a se mi je zdelo bolje, da so studiji ločeni od producentov, saj igrajo veliko večjo vlogo pri izdelavi animeja. Prav tako pa ima en anime najpogosteje zgolj en studijo, zato je bolj smiselno razporediti tabelo po studijih, kot po animejih.
