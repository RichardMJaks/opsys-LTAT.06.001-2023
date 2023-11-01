# Failiõigused Linuxis
Avastasin et pidin muutma ubuntu graafikakontrollerit, et saaksin display resizei kasutada.

## 1. Ülevaade Unixi failiõigustest
### 5-1
1. Muutmiseks läheb vaja kaustal `100` õigusi kasutajal, ning failil `600` õigusi kasutajal
2. Kustutamiseks läheb vaja kaustal `100` õigusi kasutajal ning faili `100` õigusi kasutajal

### 5-2
Selleks, et skripti tööle panna peab saama skripti ka lugeda. Kui lugemisõigus puudub, ei saa ka skripti käivitada, isegi siis kui on olemas käivitusõigus.

### 5-3 umask
Igale kasutajale luuakse omanimeline grupp selleks, et hoida kasutaja enda isiklikud failid kergesti eraldi kõikide teiste failidest. Sedasi saab kasutaja ise kontrollida oma faildie ligipääsuõigusi.

### 5-4 chown
Minimaalsed õigused et **kuvada** `uusfail.txt` sisu läheb vaja kaustal `110` õigusi et grupp ja omanik kausta sisse üldse saaks ja failil `440` et grupp ja omanik saaksid lugeda faili. Muidugi see ei luba kuvada kausta sisu, seega on vaja teada failinime, aga kuvamiseks on see minimaalne vajalik.

### setuid
#### 5-5
See on vajalik selleks, et teised kasutajad saaksid faili jooksutada omaniku õiguste raames.

#### 5-6
Jah, see vähendab süsteeemi turvalisust, sest see võib anda pahatahtlikule ründajale kõrgendatud privileegid läbi mõne faili, millel on turvavigu sees.

### Sticky bit
Faili saavad kustutada:
* kasutaja `richard` kasutades `sudo rm` käsukombinatsiooni sest ta on admin;
* kasutaja `opetaja` sest ta on kausta omanik;
* kasutaja `peeter` sest ta on faili omanik.

### ACL
\# file: tmp/klass/hinded.txt
\# owner: opetaja
\# group: opetaja
user::rw-
group::---
group:direktor:rw-
mask::rw-
other::---

### chattr
Selle faili sisu ei saa kuidagi modifitseerida.
Et kustutada seda faili peab esiteks kasutama käsku `chattr -i testfail-2` ja siis saab kustutada käsuga `rm testfail-2`
