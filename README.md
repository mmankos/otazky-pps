# Definuj a opíš
### ID_OTAZKY: 001
**Otázka**:
Definujte a opíšte čo je to granularita.

**Odpoveď**:
Granularita v kontexte paralelného spracovania označuje veľkosť (rozmer) výpočtovej úlohy, resp. množstvo práce vykonanej medzi synchronizačnými/komunikačnými bodmi. Rozlišujú sa tri základné rozmery granularity:

1. **Jemná granularita** – 2 až 1000 inštrukcií (typicky ~7 inštrukcií), využívaná paralelizujúcimi a vektorizujúcimi kompilátormi na inštrukčnej úrovni (úroveň operácie cyklu, nerekurzívny cyklus).
2. **Stredná granularita** – ~2000 inštrukcií, využívaná za pomoci programátora a čiastočne kompilátora na úrovni procedúr (multitasking, bežné subrutiny, korutiny).
3. **Hrubá granularita** – 10 000 a viac inštrukcií, využívaná pri spracovaní nezávislých hlavných programov a prác v architektúrach MIMD.

Optimalizácia granularity rieši kompromis medzi výpočtovou náročnosťou a réžiou komunikácie/synchronizácie – príliš jemná granularita zvyšuje režijné náklady, príliš hrubá znižuje možnosť paralelizácie.

---

### ID_OTAZKY: 002
**Otázka**:
Definujte a opíšte čo je to ROB a na čo slúži.

**Odpoveď**:
**ROB (Reorder Buffer)** je typ plánovacieho zásobníka (špecializovaný, decentralizovaný), ktorý sa používa v procesoroch na podporu vykonávania inštrukcií mimo poradia (out-of-order execution) pri zachovaní usporiadanej kompletizácie výsledkov.

Slúži na:
1. **Oddelenie fázy výberu inštrukcií** – eliminácia blokovania výberu inštrukcií v dôsledku údajových a zdrojových hazardov
2. **Usporiadanú kompletizáciu inštrukcií** – inštrukcie sa vykonávajú mimo poradia, ale výsledky sa kompletizujú v pôvodnom poradí programu, čím sa zabezpečuje silná procesorová konzistencia

Príklady procesorov využívajúcich ROB: Power 1 (1990), AMD K5 (1995), Pentium Pro (1995), R10000 (1996).

---

### ID_OTAZKY: 003
**Otázka**:
Čo je DRIS a na čo slúži?

**Odpoveď**:
**DRIS** je skratka pre **Deferred Scheduling, Register Renaming, Instruction Shelving** – ide o **kombinovaný plánovací zásobník** (kombinovaný P-zásobník), ktorý kombinuje deferované plánovanie, premenovávanie registrov a odkladanie inštrukcií.

Slúži na:
1. **Podporu vykonávania inštrukcií mimo poradia (out-of-order execution)** pri zachovaní usporiadanej kompletizácie výsledkov
2. **Implementáciu silnej procesorovej konzistencie** – ako alternatíva k ROB-u (ReOrder Buffer) zabezpečuje usporiadanú kompletizáciu inštrukcií v zhodnom poradí

Príklad procesora využívajúceho DRIS: Lightning (1991).

---

### ID_OTAZKY: 004
**Otázka**:
Čo je to paralelná architektúra?

**Odpoveď**:
Paralelná architektúra je línia vo vývoji počítačových architektúr, ktorá využíva paralelizmus na rôznych úrovniach na zvýšenie výkonu. Rozdeľuje sa na:

1. **Architektúry s paralelizmom riadenia** – paralelné toky inštrukcií (viacprocesorové/viacjadrové systémy, MIMD)
2. **Architektúry s dátovým paralelizmom** – vektorové procesory (SIMD)
3. **ILP architektúry (Instruction-Level Parallelism)** – paralelizmus na úrovni inštrukcií, jemnozrnný paralelizmus
4. **TLP architektúry (Thread-Level Parallelism)** – paralelizmus na úrovni vlákien

Kľúčovou otázkou paralelných architektúr je **komunikačná architektúra** – ako je komunikácia medzi procesormi integrovaná do pamäťového a I/O systému. Historicky boli paralelné architektúry úzko zviazané s programovacími modelmi a vyvíjali sa divergentne. Dnes sú viacjadrové/viacprocesorové architektúry súčasťou hlavného prúdu výpočtovej techniky a pozorujeme trend architektonickej konvergencie poháňanej technológiou, cenou a požiadavkami na aplikačný výkon.

---

### ID_OTAZKY: 005
**Otázka**:
Charakterizujte Ungererovu klasifikáciu.

**Odpoveď**:
Ungererova klasifikácia (autor Theo Ungerer) rozširuje Flynnovu taxonómiu o ďalšie kritériá na klasifikáciu paralelných počítačových architektúr:

1. **Úroveň paralelizmu** – inštrukčný (ILP), vláknový (TLP), procesový (PLP)
2. **Organizácia pamäte** – zdieľaná vs. distribuovaná
3. **Komunikačný mechanizmus** – zdieľané premenné vs. odovzdávanie správ
4. **Synchronizácia/riadenie** – synchrónne (SIMD, vektorové) vs. asynchrónne (MIMD)

Cieľom bolo presnejšie zachytiť vlastnosti moderných paralelných systémov, ktoré Flynnova klasifikácia (SISD, SIMD, MISD, MIMD) nedostatočne rozlišuje.

---

### ID_OTAZKY: 006
**Otázka**:
Definujte komunikačnú latentnosť.

**Odpoveď**:
Komunikačná latentnosť je časové oneskorenie medzi odoslaním správy/dát zo zdrojového uzla a ich prijatím cieľovým uzlom v komunikačnom systéme. Zahŕňa oneskorenia pri odosielaní (serializácia), prenose (šírenie signálu), spracovaní v sieťových prvkoch (smerovače, prepínače) a prijímaní (deserializácia, buffering).

# Urči a napíš odpoveď
### ID_OTAZKY: 007
**Kontext**:
Nech je daná postupnosť nasledujúcich inštrukcií:
1. add a, b, c
2. mul b, c, d
3. add f, g, a
4. add h, g, c
5. mul g, a, b

(Pozn. IF = <kód operácie> <cieľový operand>, <prvý zdrojový operand>, <druhý zdrojový operand>)

**Otázka**:
Určte efektívne zrýchlenie v prípade spracovania tohto prúdu inštrukcií v prúdovej funkčnej jednotke so 6-timi stupňami (Fetch, Decode, Operand address, Operand Fetch, Execute, Store).

**Odpoveď**:
2,73

**Použité premenné:**
- `n` = počet inštrukcií = 5
- `k` = počet stupňov pipeline = 6 (Fetch, Decode, Operand address, Operand Fetch, Execute, Store)
- `T_s` = čas vykonania pri sekvenčnom spracovaní (inštrukcie sa vykonávajú jedna po druhej)
- `T_p` = čas vykonania pri prúdovom spracovaní (pipeline)
- `stalls` = počet vložených čakacích cyklov kvôli hazardom

**Dôležitá poznámka:** V jednoduchej skalárnej in-order pipeline riešime **iba RAW hazardy** (Read After Write). WAR (Write After Read) a WAW (Write After Write) v tomto režime nastať nemôžu, pretože inštrukcie sa spracúvajú v poradí — OF (4. stupeň) je vždy pred S (6. stupeň) tej istej inštrukcie a S predchádzajúcej inštrukcie je vždy pred S nasledujúcej. Stall je potrebný, keď OF závislej inštrukcie nastane v rovnakom alebo skoršom cykle ako S produkčnej inštrukcie (výsledok je v registri dostupný až po S, nie po E).

**Sekvenčný čas** — každá inštrukcia trvá `k` cyklov, vykonávajú sa za sebou:
$$T_s = n \times k = 5 \times 6 = 30\ \text{cyklov}$$

**Prúdový čas (ideálny, bez hazardov)** — prvá inštrukcia trvá `k` cyklov, každá ďalšia sa dokončí o 1 cyklus neskôr:
$$T_{\text{p(ideál)}} = k + (n - 1) = 6 + 4 = 10\ \text{cyklov}$$

**RAW hazardy v postupnosti:**
- I1: `add a, b, c` → cieľ `a` (zapisuje v S – 6. stupeň)
- I2: `mul b, c, d` → cieľ `b` (zapisuje v S)
- I3: `add f, g, a` → číta `a` v OF (4. stupeň), ktorý zapisuje I1. I1 zapíše `a` v cykle 6, I3 by chcelo čítať v cykle 6 → RAW hazard → **1 stall**
- I5: `mul g, a, b` → číta `a` (z I1, S v cykle 6) a `b` (z I2, S v cykle 7) v OF v cykle 9 → hodnoty sú už zapísané → **bez stallu**

**Časovanie s hazardmi (6-stupňová pipeline: F, D, OA, OF, E, S):**
```
Cyklus:  1   2   3   4   5   6   7   8   9  10  11
I1:      F   D   OA  OF  E   S
I2:          F   D   OA  OF  E   S
I3:              F   D   OA  st  OF  E   S
I4:                  F   D   D   OA  OF  E   S
I5:                      F   F   D   OA  OF  E   S
```
(st = stall — I3 čaká v OA, I4 a I5 sú blokované, lebo predchádzajúci stupeň je obsadený)

**Prúdový čas (reálny):**
$$T_p = k + (n - 1) + \text{stalls} = 6 + 4 + 1 = 11\ \text{cyklov}$$

**Efektívne zrýchlenie:**
$$\text{Speedup} = \frac{T_s}{T_p} = \frac{30}{11} \approx 2{,}73$$

---

### ID_OTAZKY: 008
**Kontext**:
SM GPU dokáže spracovať maximálne 2048 vlákien. Kernel používa bloky veľkosti 256 vlákien a na SM môže bežať 6 blokov.

**Otázka**:
Aká je obsadenosť výpočtových zdrojov (angl. occupancy) v percentách? Znak % neuvádzajte!

**Odpoveď**:
75

**Postup výpočtu:**

- `max_vlakien` = maximálny počet vlákien, ktoré SM zvládne = 2048
- `velkost_bloku` = počet vlákien v jednom bloku = 256
- `max_blokov` = maximálny počet blokov na SM = 6

**Skutočný počet vlákien na SM:**
$$\text{skutočné vlákna} = \text{veľkosť bloku} \times \text{max blokov} = 256 \times 6 = 1536$$

**Obsadenosť (occupancy):**
$$\text{occupancy} = \frac{\text{skutočné vlákna}}{\text{max vlákien}} \times 100\ \% = \frac{1536}{2048} \times 100\ \% = 75\ \%$$

Obmedzujúcim faktorom je počet blokov — pri 256 vláknach na blok by naplnenie kapacity 2048 vlákien vyžadovalo 8 blokov, ale SM zvládne len 6.

---

### ID_OTAZKY: 009
**Kontext**:
```
int sum_array_rows(int a[M][N]) {
  int i, j, sum = 0;
  for (i = 0; i < M; i++)
    for (j = 0; j < N; j++)
      sum += a[i][j];
  return sum;
}
```
Za predpokladu, že pre lokálne premenné tejto funkcie boli vyhradené registre, sizeof(int)=32b a veľkosť rámu bloku v pamäti cache je 128b.

**Otázka**:
Určte hodnotu neúspešného hľadania (miss rate) v plne asociatívnej pamäti bezprostredne po prvom zavolaní funkcie. Hodnotu zadajte v percentách - ako celé číslo - bez uvedenia znaku %.

**Odpoveď**:
25

**Postup výpočtu:**

- `sizeof(int)` = 32 bitov
- Veľkosť bloku cache = 128 bitov
$$\text{počet intov v bloku} = \frac{128}{32} = 4$$

Pri sekvenčnom prístupe:
- Prvý prístup ku každému bloku je **miss** (compulsory miss) — načíta sa celý 128b blok do cache
- Ďalšie 3 prístupy k prvkom v tom istom bloku sú **hit**

$$\text{počet prístupov} = M \times N$$

$$\text{počet missov} = \frac{\text{počet prvkov}}{\text{prvkov na blok}} = \frac{M \times N}{4}$$

(jeden miss na každý blok — do jedného bloku sa zmestia 4 inty)

Hodnoty M a N nie sú zadané, ale nie sú potrebné — vo vzorci sa vykrátia:

$$\text{miss rate} = \frac{\text{počet missov}}{\text{počet prístupov}} = \frac{\frac{M \times N}{4}}{M \times N} = \frac{1}{4} = 0{,}25 = 25\%$$

Miss rate závisí výhradne od pomeru veľkosti bloku cache a veľkosti prvku poľa, nie od rozmerov poľa.

---

### ID_OTAZKY: 010
**Kontext**:
Nech je daný dvojúrovňový pamäťový podsystém (cache a hlavná pamäť). Prístupová doba pamäte cache je 1 strojový cyklus (angl. cache hit time), prístupová doba hlavnej pamäte je 100 strojových cyklov (angl. miss penalty).

**Otázka**:
Pri akej hodnote úspešného hľadania v cache (angl. hit rate; h) získame trikrát dlhšiu priemernú prístupovú dobu ako bolo namerané pri h = 99%? Vašu odpoveď uveďte ako celé číslo bez uvedenia znaku %.

**Odpoveď**:
95

**Postup výpočtu:**

Vzorec pre priemernú prístupovú dobu (AMAT):
$$\text{AMAT} = \text{hit time} + \text{miss rate} \times \text{miss penalty}$$

kde:
- `hit time` = prístupová doba cache = 1 cyklus
- `miss penalty` = prístupová doba hlavnej pamäte = 100 cyklov
- `miss rate` = 1 - h

**1. AMAT pri h = 99% (0,99):**
$$\text{miss rate} = 1 - 0{,}99 = 0{,}01$$
$$\text{AMAT}_{99} = 1 + 0{,}01 \times 100 = 1 + 1 = 2\ \text{cykly}$$

**2. Hľadáme h také, aby AMAT = 3 × AMAT pri 99%:**
$$\text{AMAT}_h = 3 \times 2 = 6\ \text{cyklov}$$

**3. Dosadenie do vzorca:**
$$1 + (1 - h) \times 100 = 6$$
$$(1 - h) \times 100 = 5$$
$$1 - h = 0{,}05$$
$$h = 0{,}95 = 95\%$$

---

### ID_OTAZKY: 011
**Kontext**:
Rezervačná tabuľka

| S/T | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **S3** | x |   |   |   |   | x |   | x |
| **S2** |   | x |   | x |   |   |   |   |
| **S1** |   |   | x |   | x |   | x |   |

**Otázka**:
Určte počiatočný vektor kolízií ($C^0 = C_0C_1C_2...C_n$) na základe rezervačnej tabuľky. Vektor $C^0$ zapíšte v podobe čísla; medzi číslicami nesmú byť medzery.

**Odpoveď**:
10101101

**Postup riešenia:**

1. **Pochopenie rezervačnej tabuľky** – riadky predstavujú stupne (S1–S3 pipeline), stĺpce predstavujú časové cykly (1–8). Značka "x" v bunke znamená, že daný stupeň je v danom cykle využitý.

2. **Identifikácia zaplnených buniek v každom riadku:**
   - S3: cykly 1, 6, 8
   - S2: cykly 2, 4
   - S1: cykly 3, 5, 7

3. **Výpočet zakázaných latencií** – pre každý riadok zvlášť vypočítame rozdiely medzi všetkými dvojicami zaplnených cyklov:
   - S3: |6-1|=5, |8-1|=7, |8-6|=2 → {2, 5, 7}
   - S2: |4-2|=2 → {2}
   - S1: |5-3|=2, |7-3|=4, |7-5|=2 → {2, 4}

4. **Zjednotenie** – všetky zakázané latencie: {2, 4, 5, 7}

5. **Zostavenie vektora** – $C^0 = C_0C_1C_2...C_7$, kde $C_0=1$ (latencia 0 je vždy kolízia). Platí: $C_k = 1$ ak je latencia $k$ zakázaná (spôsobuje kolíziu), inak $C_k = 0$.

   | Latenica k | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
   |-----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
   | C_k       | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 1 |

   $C^0 = C_0C_1C_2C_3C_4C_5C_6C_7 = 10101101$

---

### ID_OTAZKY: 012
**Kontext**:
Rezervačná tabuľka

| S/T | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **S4** | x |   |   |   |   | x |
| **S3** |   | x |   |   |   |   |
| **S2** |   |   | x |   |   |   |
| **S1** |   |   |   | x | x |   |

**Otázka**:
Určte počiatočný vektor kolízií ($C^0 = C_0C_1C_2...C_n$) na základe nasledujúcej rezervačnej tabuľky:
Vektor $C^0$ zapíšte v podobe čísla; medzi číslicami nesmú byť medzery.

**Odpoveď**:
110001

**Postup riešenia:**

1. **Identifikácia zaplnených buniek v každom riadku:**
   - S4: cykly 1, 6
   - S3: cykly 2
   - S2: cykly 3
   - S1: cykly 4, 5

2. **Výpočet zakázaných latencií** – pre každý riadok zvlášť vypočítame rozdiely medzi všetkými dvojicami zaplnených cyklov:
   - S4: |6-1| = 5 → {5}
   - S3: iba jedna bunka → {}
   - S2: iba jedna bunka → {}
   - S1: |5-4| = 1 → {1}

3. **Zjednotenie** – všetky zakázané latencie: {1, 5}

4. **Zostavenie vektora** – $C^0 = C_0C_1C_2...C_5$, kde $C_0=1$ (latencia 0 je vždy kolízia). Platí: $C_k = 1$ ak je latencia $k$ zakázaná (spôsobuje kolíziu), inak $C_k = 0$.

   | Latenica k | 0 | 1 | 2 | 3 | 4 | 5 |
   |-----------|:-:|:-:|:-:|:-:|:-:|:-:|
   | C_k       | 1 | 1 | 0 | 0 | 0 | 1 |

   $C^0 = C_0C_1C_2C_3C_4C_5 = 110001$

---

### ID_OTAZKY: 013
**Kontext**:
Nech je daný počítačový systém pracujúci na taktovacej frekvencii 2.0GHz vybavený lineárnym 6 stupňovým systémom zreťazenia. Počas spracovania prúdu 8 po sebe nasledujúcich inštrukcií došlo k detekcii dvoch dátových hazardov typu RAW. Riešenie prvého hazardu je spojené s oneskorením 2 strojových cyklov, riešenie druhého hazardu s oneskorením 1 strojového cyklu. Aké je efektívne zrýchlenie systému?

**Otázka**:
Určte efektívne zrýchlenie počítačového systému!
Hodnotu efektívneho zrýchlenia zaokrúhlite na stotiny!

**Odpoveď**:
3,00

**Postup výpočtu:**

**Sekvenčný čas** — každá z 8 inštrukcií trvá 6 cyklov:
$$T_s = n \times k = 8 \times 6 = 48\ \text{cyklov}$$

**Prúdový čas (ideálny, bez hazardov)** — prvá inštrukcia trvá 6 cyklov, každá ďalšia o 1 cyklus neskôr:
$$T_{\text{p(ideál)}} = k + (n - 1) = 6 + 7 = 13\ \text{cyklov}$$

**Prúdový čas (reálny)** — s dvomi RAW hazardmi (2 + 1 stall):
$$T_p = k + (n - 1) + \text{stalls} = 6 + 7 + 3 = 16\ \text{cyklov}$$

**Efektívne zrýchlenie:**
$$\text{Speedup} = \frac{T_s}{T_p} = \frac{48}{16} = 3{,}00$$

# Výber z možností
## Skupina: Inštrukčné závislosti

### ID_OTAZKY: 014
**Typ**: Single-Choice (Select ONE)

**Kontext**:

| # | Inštrukcia | Význam |
|---|---|---|
| i1 | load RG1, M[A] | RG1 := M[A] |
| i2 | store M[B], RG1 | M[B] := RG1 |

**Otázka**:
Medzi inštrukciami i1 a i2 je závislosť typu? Označte jednu odpoveď.

**Odpoveď**:
- [X] RAW
- [ ] WAW
- [ ] WAR
- [ ] riadiaca závislosť

**Vysvetlenie**:
i1 zapisuje do RG1, i2 číta RG1 → RAW (Read After Write) hazard.

### ID_OTAZKY: 015
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Nech je daná postupnosť nasledujúcich inštrukcií

1. add a, b, c
2. mul c, b, d
3. add f, g, a
4. add h, g, c
5. mul g, a, b

( Pozn. IF = <kód operácie> <cieľový operand>,<prvý zdrojový operand>,<druhý zdrojový operand> )

**Otázka**:
Označte správne odpovede!

**Odpoveď**:
- [ ] Dvojica inštrukcií (3, 5) môže byť vykonaná paralelne.
- [x] Dvojica inštrukcií (2, 5) môže byť vykonaná paralelne.
- [ ] Dvojica inštrukcií (1, 3) môže byť vykonaná paralelne.
- [x] Dvojica inštrukcií (2, 3) môže byť vykonaná paralelne.

**Vysvetlenie**:
- (3, 5): 3 číta g, 5 zapisuje g → **WAR hazard** → ❌ Nie
- (2, 5): 2 číta b, 5 číta b (RR) a 2 zapisuje c, 5 zapisuje g → žiadna zdieľaná premenná → ✅ Áno
- (1, 3): 1 zapisuje a, 3 číta a → **RAW hazard** → ❌ Nie
- (2, 3): 2 zapisuje c, 3 číta g, a → žiadna zdieľaná premenná → ✅ Áno

### ID_OTAZKY: 016
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Nech je daná postupnosť nasledujúcich príkazov:
1. $A = D + 2$
2. $E = C - D$
3. $B = A \times C$
4. $C = A + B$
5. $D = 4 \times B$

**Otázka**:
Označte správne tvrdenia:

**Odpoveď**:
- [x] Medzi príkazom 3 a 4 je hazard typu WAR.
- [x] Medzi príkazom 1 a 5 je hazard typu WAR.
- [ ] Medzi príkazom 1 a 3 je hazard typu WAW.
- [ ] Medzi príkazom 4 a 5 je hazard typu WAR.
- [x] Medzi príkazom 1 a 4 je hazard typu RAW.
- [x] Medzi príkazom 1 a 3 je hazard typu RAW.

**Vysvetlenie**:
- **3→4 WAR**: 3 číta **C**, 4 zapisuje **C** ✓
- **1→5 WAR**: 1 číta **D**, 5 zapisuje **D** ✓
- **1→3 WAW**: 1 zapisuje A, 3 zapisuje B — rôzne registre ✗
- **4→5 WAR**: 4 číta A,B; 5 zapisuje D — žiadny prienik ✗
- **1→4 RAW**: 1 zapisuje **A**, 4 číta **A** ✓
- **1→3 RAW**: 1 zapisuje **A**, 3 číta **A** ✓

---

## Skupina: Vektorizácia

**Všeobecné vzorce:**

- $T_s = T_{s,\text{nonvec}} + T_{s,\text{vec}}$
- $T_{s,\text{nonvec}} = N_{\text{nonvec}} \times t_{\text{scalar}}$
- $T_{s,\text{vec}} = N_{\text{iter}} \times t_{\text{body}}$
- $T_v = T_{s,\text{nonvec}} + \dfrac{T_{s,\text{vec}}}{\eta_v}$
- $K = \dfrac{T_s}{T_v}$ – koeficient účinnosti vektorizácie
- $r = \dfrac{T_{s,\text{vec}}}{T_s}$ – koeficient vektorizácie

kde:
- $N_{\text{nonvec}}$ – počet skalárnych operácií v nevektorizovateľnej časti
- $t_{\text{scalar}}$ – doba vykonania jednej skalárnej operácie
- $N_{\text{iter}}$ – počet iterácií logického cyklu
- $t_{\text{body}}$ – doba vykonania tela cyklu
- $\eta_v$ – účinnosť vektorového spracovania

### ID_OTAZKY: 017
**Typ**: Single-Choice (Select ONE)

**Kontext**:
- Nevektorizovateľná časť programu: 5 skalárnych operácií,
- Doba vykonania jednej skalárnej operácie: 6 strojových cyklov (SC)
- Vektorizovateľná časť programu: 1 operácia 10-násobného logického cyklu
- Doba vykonania tela cyklu: 25 SC
- Účinnosť vektorového spracovania: 3,06

**Otázka**:
Koeficient účinnosti vektorizácie pre nasledujúcu skladbu programu sa rovná:

**Odpoveď**:
- [X] 2,50
- [ ] 3,23
- [ ] 3,11
- [ ] 2,62

**Výpočet**:
- $N_{\text{nonvec}} = 5$
- $t_{\text{scalar}} = 6$ SC
- $N_{\text{iter}} = 10$
- $t_{\text{body}} = 25$ SC
- $\eta_v = 3,06$

- $T_{s,\text{nonvec}} = N_{\text{nonvec}} \times t_{\text{scalar}} = 5 \times 6 = 30$ SC
- $T_{s,\text{vec}} = N_{\text{iter}} \times t_{\text{body}} = 10 \times 25 = 250$ SC
- $T_s = T_{s,\text{nonvec}} + T_{s,\text{vec}} = 30 + 250 = 280$ SC

- $T_v =T_{s,\text{nonvec}} + \dfrac{T_{s,\text{vec}}}{\eta_v} = 30 + \dfrac{250}{3,06} \approx 111{,}70$ SC
- $K = \frac{T_s}{T_v} = \frac{280}{111{,}70} \approx 2{,}51$
- Najbližšia možnosť je **2,50**.

### ID_OTAZKY: 018
**Typ**: Single-Choice (Select ONE)

**Kontext**:
- Nevektorizovateľná časť programu: 5 skalárnych operácií,
- Doba vykonania jednej skalárnej operácie: 6 strojových cyklov (SC)
- Vektorizovateľná časť programu: 1 operácia 10-násobného logického cyklu
- Doba vykonania tela cyklu: 25 SC
- Účinnosť vektorového spracovania: 5,00

**Otázka**:
Určte koeficient vektorizácie pre nasledujúce hodnoty:

**Odpoveď**:
- [ ] r = 4,20
- [X] r = 0,89
- [ ] r = 0,31
- [ ] r = 2,50

**Výpočet**:
- $N_{\text{nonvec}} = 5$
- $t_{\text{scalar}} = 6$ SC
- $N_{\text{iter}} = 10$
- $t_{\text{body}} = 25$ SC
- $\eta_v = 5,00$

- $T_{s,\text{nonvec}} = 5 \times 6 = 30$ SC
- $T_{s,\text{vec}} = 10 \times 25 = 250$ SC
- $T_s = 30 + 250 = 280$ SC

- $r = \frac{T_{s,\text{vec}}}{T_s} = \frac{250}{280} \approx 0{,}89$

---

### ID_OTAZKY: 019
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Koeficient účinnosti vektorizácie pre nasledujúcu skladbu programu
Nevektorizovateľná časť programu: 5 skalárnych operácií,
Doba vykonania jednej skalárnej operácie: 8 strojových cyklov (SC)
Vektorizovateľná časť programu: 1 operácia 10-násobného logického cyklu
Doba vykonania tela cyklu: 25 SC
Účinnosť vektorového spracovania: 4,17
sa rovná:

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [ ] 2,62
- [ ] 3,11
- [ ] 3,23
- [X] 2,90

**Výpočet**:
- $N_{\text{nonvec}} = 5$
- $t_{\text{scalar}} = 8$ SC
- $N_{\text{iter}} = 10$
- $t_{\text{body}} = 25$ SC
- $\eta_v = 4,17$

- $T_{s,\text{nonvec}} = N_{\text{nonvec}} \times t_{\text{scalar}} = 5 \times 8 = 40$ SC
- $T_{s,\text{vec}} = N_{\text{iter}} \times t_{\text{body}} = 10 \times 25 = 250$ SC
- $T_s = T_{s,\text{nonvec}} + T_{s,\text{vec}} = 40 + 250 = 290$ SC

- $T_v = T_{s,\text{nonvec}} + \dfrac{T_{s,\text{vec}}}{\eta_v} = 40 + \dfrac{250}{4,17} \approx 99,95$ SC
- $K = \frac{T_s}{T_v} = \frac{290}{99,95} \approx 2,90$

- merged-pps.pdf strana 480–482: princíp vektorizácie a vzorový príklad s rovnakou skladbou programu (5 skalárnych operácií, 10-násobný cyklus).

---

## Skupina: Klasifikácia architektúr (Flynn)

### ID_OTAZKY: 020
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Charakteristika architektúr MIMD.

**Otázka**:
Označte výrok (resp. výroky), ktoré považujete za pravdivé.

**Odpoveď**:
- [ ] Nie je správny ani jeden z uvedených výrokov o MIMD.
- [x] Má N riadiacich jednotiek a M vykonávacích jednotiek.
- [ ] Má 1 riadiacu jednotku a M vykonávacích jednotiek.
- [ ] Príkladom architektúry MIMD sú počítače podľa pôvodného von Neumannovského konceptu počítačov.

### ID_OTAZKY: 021
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Dokončte nasledujúcu vetu.
Údajový prúd spracúvaný v lineárnom procesorovom poli viacnásobným inštrukčným prúdom pozostávajúcim z rozličných inštrukcií pre jednotlivé procesné elementy je charakteristický pre architektúru typu:

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] MIMD
- [ ] SIMD
- [ ] SISD
- [X] MISD

**Vysvetlenie**:
Kontext hovorí *"viacnásobným inštrukčným prúdom"* → pri I je M (Multiple). *"Údajový prúd"* (jednotné číslo) → pri D je S (Single). Preto MISD.

### ID_OTAZKY: 022
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Ktorý výrok je pravdivý ohľadom SISD architektúr?

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] Má N riadiacich jednotiek a M vykonávacích jednotiek.
- [ ] Má N riadiacich jednotiek a 1 vykonávaciu jednotku.
- [X] Má 1 riadiacu jednotku a 1 vykonávaciu jednotku.
- [ ] Má 1 riadiacu jednotku a M vykonávacích jednotiek.

**Vysvetlenie**:
- merged-pps.pdf strana 163: *"Jedna riadiaca jednotka (RJ), Jedna vykonávacia jednotka (VJ), Čítanie/zápis do pamäte len jednej hodnoty."*

---

## Skupina: Tok dát (Dataflow)

### ID_OTAZKY: 023
**Typ**: Multiple-Choice (Select ONE or MANY)

**Otázka**:
Ktoré výroky sú pravdivé o DF architektúrach?

**Odpoveď**:
- [ ] Model toku dát disponuje spoločnými prepisovatellnými parnëťovými elementmi.
- [x] Model toku dát nedisponuje spoločnými prepisovatel'nými pamaťovými elementmi.
- [x] Poradie inštrukcií v programe nemá vplyv na poradie vykonávania týchto inštrukcií.
- [ ] Poradie inštrukcií v programe má vplyv na poradie vykonávania týchto inštrukcií.

### ID_OTAZKY: 024
**Typ**: Single-Choice (Select ONE)

**Kontext**:
V súvislosti s počítačmi riadenými tokom dát je alebo nie je nasledujúci výrok pravdivý?
Inštrukcia je vykonateľná, ak všetky jej operandy sú prístupné.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [x] Pravda
- [ ] Nepravda

**Vysvetlenie**:
Toto je **Pravidlo vykonateľnosti (PV)** pre počítače riadené tokom dát (dataflow). Inštrukcia sa aktivuje až vtedy, keď sú na jej vstupoch prítomné všetky operandy (aktivačné značky). (lecture-database chunk 787)

### ID_OTAZKY: 025
**Typ**: Single-Choice (Select ONE)

**Kontext**:
V súvislosti s počítačmi riadenými tokom dát je alebo nie je nasledujúci výrok pravdivý?
Inštrukcia je vykonateľná, ak všetky jej operandy sú prístupné.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

**Vysvetlenie**:
- Toto je **Pravidlo vykonateľnosti (PV)** pre počítače riadené tokom dát (dataflow).
- merged-pps.pdf strana 919: Inštrukcia sa aktivuje až vtedy, keď sú na jej vstupoch prítomné všetky operandy (aktivačné značky).

### ID_OTAZKY: 026
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Ktorý výrok, resp. výroky sú pravdivé ohľadom DF architektúr?

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [ ] Sú to počítače riadené tokom príkazov.
- [ ] Komunikácia medzi procesmi je zabezpečená jedine za pomoci spoločného pamäťového priestoru.
- [x] Procesy komunikujú prostredníctvom správ.
- [x] Radenie je založené na interpretácii toku dát.

**Vysvetlenie**:
- merged-pps.pdf strana 582: **Sú to počítače riadené tokom príkazov.** → ✗ DF je riadený **tokom dát**, nie tokom príkazov (to je CF model). V DF modeli platí: *"Inštrukcia sa vykoná vtedy ak sú dostupné všetky informácie (všetky operandy) na jej vykonanie."*
- merged-pps.pdf strana 582: **Komunikácia medzi procesmi je zabezpečená jedine za pomoci spoločného pamäťového priestoru.** → ✗ *"Model toku dát nedisponuje spoločnými prepisovateľnými pamäťovými elementmi."*
- merged-pps.pdf strana 110: **Procesy komunikujú prostredníctvom správ.** → ✓ V DF architektúrach sa tok dát realizuje formou **správ (tokenov)** medzi procesormi: *"Správy (tokeny) nesú značku (tag) nasledujúcej inštrukcie a posielajú sa do ďalšieho procesora."*.
- merged-pps.pdf strana 582: **Radenie je založené na interpretácii toku dát.** → ✓ *"Poradie inštrukcií v programe nemá vplyv na poradie vykonávania týchto inštrukcií."*

---

## Skupina: Frekvencia a teplo CPU

**Všeobecné vysvetlenie:**

Dynamický výkon (teplo) v CMOS obvodoch je daný vzťahom:

$$P = \alpha \cdot C \cdot V^2 \cdot f$$

kde:
- $\alpha$ – aktivitný faktor
- $C$ – kapacitná záťaž
- $V$ – napájacie napätie
- $f$ – taktovacia frekvencia

Pri zdvojnásobení frekvencie ($f \to 2f$) je zvyčajne potrebné zvýšiť aj napätie, aby obvod stíhal spínať pri vyššej frekvencii. V praxi platí približne $V \propto f$, teda $V \to 2V$.

$$P_{\text{new}} = C \cdot (2V)^2 \cdot (2f) = C \cdot 4V^2 \cdot 2f = 8 \cdot C \cdot V^2 \cdot f = 8 \cdot P_{\text{old}}$$

Výkon (a teda generované teplo) vzrastie približne **8-násobne** ($2^3 = 8$).

### ID_OTAZKY: 027
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Ak zvýšime taktovaciu frekvenciu CPU na dvojnásobok, CPU bude generovať približne.

**Otázka**:
Označte jednu odpoveď

**Odpoveď**:
- [ ] 2-krát viac tepla
- [ ] 3-krát viac tepla
- [ ] 6-krát viac tepla
- [X] 8-krát viac tepla (táto možnosť je na obrázku označená)

### ID_OTAZKY: 028
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý?
Ak zvýšime taktovaciu frekvenciu CPU na dvojnásobok, CPU bude generovať cca. 2-krát viac tepla.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [ ] Pravda
- [x] Nepravda

### ID_OTAZKY: 029
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý?
Medzi nárastom počtu tranzistorov tvoriacich CPU a nárastom taktovacej frekvencie je nepriama úmera.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [ ] Pravda
- [X] Nepravda

**Vysvetlenie**:
Výrok je nepravdivý. Historicky (1971 – cca 2005) rástol počet tranzistorov aj taktovacia frekvencia súčasne (priama úmera). Neskôr síce frekvencia stagnovala, kým tranzistory naďalej pribúdali, ale nejde o nepriamu úmeru – frekvencia neklesá úmerne s rastom tranzistorov.
- merged-pps.pdf strana 4: *"Paralelizmus predstavuje alternatívu k zvyšovaniu taktovacej frekvencie pri zvyšovaní výkonu."* – Paralelizmus (viac tranzistorov) nahrádza zvyšovanie frekvencie, ale frekvencia neklesá.
- merged-pps.pdf strana 200: *"Rádové zvýšenie taktovacej frekvencie procesorov. Významný nárast počtu tranzistorov."* – V historickom kontexte rástli obe veličiny súbežne.

---

## Skupina: Paralelné programovanie (CUDA, OpenMP, vlákna)

### ID_OTAZKY: 030
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Uvažujte CUDA zariadenie (8 blokov/SM, 1024 vlákien/SM).

**Otázka**:
Ktoré tvrdenia o obsadenosti výpočtových zdrojov (angl. occupancy) sú správne?

**Odpoveď**:
- [ ] Maximálna obsadenosť výpočtových zdrojov vždy znamená maximálny výkon.
- [ ] Obsadenosť výpočtových zdrojov nemá vplyv na výkon.
- [x] Vyššia obsadenosť výpočtových zdrojov zlepšuje schopnosť skrývať latenciu.
- [x] Obsadenosť výpočtových zdrojov je pomer aktívnych warpov (resp. vlákien) k maximálnemu počtu warpov (resp. vlákien).
- [x] Príliš nízka obsadenosť výpočtových zdrojov vedie k nevyužitiu zdrojov.

### ID_OTAZKY: 031
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Ak sa program skompiluje bez podpory OpenMP (bez prepínača -fopenmp).

**Otázka**:
Čo sa stane s direktívou #pragma omp parallel for ?

**Odpoveď**:
- [ ] Kompilátor automaticky vytvorí vlákna pomocou POSIX threads.
- [ ] Program sa neskompiluje.
- [x] Direktíva je ignorovaná a cyklus sa vykoná sekvenčne.
- [ ] Program sa spustí paralelne pomocou systémového scheduleru.

### ID_OTAZKY: 032
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Určte pravdivosť tvrdenia.
Funkciu pthread_join voláme raz pre každé vlákno.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

**Vysvetlenie**:
- merged-pps.pdf strana 636: *"We call the function pthread_join once for each thread."*

---

### ID_OTAZKY: 033
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Majme 3 vlákna; vlákno s identifikátorom ID0, vlákno s ID1 a vlákno s ID2. Potom pri vykonaní nasledujúceho fragmentu kódu:

```
sum = 0.0;
#pragma omp parallel for num_threads(3) reduction(+: sum) schedule(static, 1)
for (i = 0; i < 12; i++)
    sum += f(i);
```

**Otázka**:
vlákno s ID0 spracováva funkcie:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] f(0), f(3), f(6), f(9)
- [ ] f(2), f(3), f(8), f(9)
- [ ] f(0), f(1), f(2), f(3)
- [ ] f(1), f(4), f(7), f(10)

**Vysvetlenie**:
Pre `schedule(static, 1)` s 3 vláknami a 12 iteráciami (0–11) sa iterácie rozdeľujú cyklicky (round-robin) po 1:
- **ID0**: 0, 3, 6, 9
- ID1: 1, 4, 7, 10
- ID2: 2, 5, 8, 11

Správna odpoveď je `f(0), f(3), f(6), f(9)`.

- merged-pps.pdf strana 799: *"Cyclic schedule: schedule(static, 1)"*
- merged-pps.pdf strana 801: *"schedule (static, 1) — Thread 0: 0,3,6,9 | Thread 1: 1,4,7,10 | Thread 2: 2,5,8,11"*

---

### ID_OTAZKY: 034
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Označte kľúčové slová dostupné v CUDA!

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [x] blockIdx
- [ ] processIdx
- [x] threadIdx
- [ ] cernelIdx

**Vysvetlenie**:
- merged-pps.pdf strana 946: *"CUDA kernels have access to two more built-in variables (threadIdx, blockIdx)"*

---

### ID_OTAZKY: 035
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Majme **3 vlákna**; vlákno s identifikátorom ID 0, vlákno s ID 1, a vlákno s ID 2.
Potom po vykonaní nasledujúceho fragmentu kódu
```
sum = 0.0;
#pragma omp parallel for \
num_threads(thread_count) reduction(+: sum) \
schedule(static, 2)
for (i = 0; i < 12; i++)
    sum += f(i);
```
vlákno s ID 0 spracováva funkcie:

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] f(1), f(4), f(7), f(11)
- [ ] f(0), f(1), f(2), f(3)
- [ ] f(0), f(3), f(5), f(7)
- [X] f(0), f(1), f(6), f(7)

**Vysvetlenie**:
Pre `schedule(static, 2)` s 3 vláknami a 12 iteráciami (0–11) sa iterácie rozdelia do blokov po 2 a priradia cyklicky:
- Iterácie rozdelené na 6 blokov po 2: `[0,1]`, `[2,3]`, `[4,5]`, `[6,7]`, `[8,9]`, `[10,11]`
- **Thread 0**: blok 0 → `[0,1]`, blok 3 → `[6,7]` → **f(0), f(1), f(6), f(7)**
- Thread 1: blok 1 → `[2,3]`, blok 4 → `[8,9]`
- Thread 2: blok 2 → `[4,5]`, blok 5 → `[10,11]`

---

## Skupina: Programovacie modely (MP, SAS)

### ID_OTAZKY: 036
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Ktorý výrok je pravdivý ohľadom MP programovacieho modelu?

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] Komunikácia medzi procesmi je zabezpečená výlučne pomocou spoločného pamäťového priestoru.
- [X] Procesy komunikujú prostredníctvom správ.
- [ ] Tvorí základ pre počítače riadené tokom dát.
- [ ] Radenie je zavedené na interpretácii toku dát.

**Vysvetlenie**:
MP (Message Passing) programovací model je založený na explicitnej komunikácii procesov prostredníctvom správ — nejde o zdieľanú pamäť, ale o odovzdávanie správ (ako listy alebo telefonáty). Tento model nemá zdieľaný adresný priestor a procesy komunikujú bod-bod pomocou operácií `send` a `receive`.

- merged-pps.pdf strana 255: *"Programovací model odovzdávania správ (message passing)"*, *"Neexistuje zdieľaný adresný priestor."*
- merged-pps.pdf strana 74: *"Odovzdávanie správ – ako listy alebo telefonáty, explicitná bod-bod komunikácia"*
- merged-pps.pdf strana 256: *"Send a receive môžu zabezpečiť bod-bod synchronizáciu medzi procesmi"*

---

### ID_OTAZKY: 037
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Ktorý výrok je pravdivý ohľadom SAS programovacieho modelu?

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [X] Komunikácia medzi procesmi (vláknami) je zabezpečená pomocou spoločného pamäťového priestoru.
- [ ] Radenie je založené na interpretácii toku dát.
- [ ] Procesy komunikujú prostredníctvom správ.
- [ ] Tvorí základ pre počítače riadené tokom dát.

**Vysvetlenie**:
SAS (Shared Address Space – zdieľaný adresný priestor) je programovací model, v ktorom procesy/vlákna komunikujú prostredníctvom spoločného pamäťového priestoru (ako "nástenka" – bulletin board). Nejedná sa o odovzdávanie správ (MP model) ani o tok dát (dataflow).

- merged-pps.pdf strana 254: *"Programovací model so zdieľaným adresným priestorom (SAS)"*, *"Každý proces môže pomenovať ľubovoľnú premennú v zdieľanom priestore."*
- merged-pps.pdf strana 74: *"Zdieľaný adresný priestor – ako nástenka (bulletin board)"*

---

## Skupina: Architektúry a modely vykonávania (ILP, TLP, VLIW, superskalárne)

### ID_OTAZKY: 038
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý?
Pri načítaní operandov vo fáze Výberu (angl. Issue) tak pamäť registrov ako aj P-zásobník obsahuje informáciu o platnosti obsahu príslušného zdrojového registra.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

**Vysvetlenie**:
- merged-pps.pdf strana 559: *"Pri načítaní operandov vo fáze Výberu tak pamäť registrov ako aj P-zásobník obsahuje informáciu o platnosti obsahu príslušného zdrojového (resp. cieľového) registra."*

### ID_OTAZKY: 039
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Nasledujúca postupnosť
$(I_{11}), (I_{21}), \dots, (I_{n1}), (I_{12}), (I_{22}), \dots, (I_{n2}), \dots (I_{13}), (I_{23}), \dots, (I_{n3}), \dots$
kde $I_{jk}$ je k-ta inštrukcia j-tého vlákna opisuje vykonanie inštrukcií

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] v skalárnych procesoroch s blokovým prekrývaním inštrukcií.
- [X] v skalárnych procesoroch s cyklickým prekrývaním inštrukcií.

**Vysvetlenie**:
- merged-pps.pdf strana 532: Skalárne procesory s cyklickým prekrývaním (prvé tri inštrukcie) $(I_{11}), (I_{21}), \dots , (I_{n1}), (I_{12}), \dots , (I_{n2}), \dots , (I_{13}), \dots , (I_{n3}), \dots$
- merged-pps.pdf strana 602: Pre blokové prekrývanie by postupnosť bola $(I_{11}), (I_{12}), \dots , (I_{1n_1}), (I_{21}), \dots$

### ID_OTAZKY: 040
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Ktorý výrok, resp. výroky sú pravdivé?

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [ ] Paralelné spracovania „dát“ v ILP procesoroch sa uskutočňuje aplikovaním princípu zvyšovania počtu funkčných jednotiek.
- [ ] Paralelné spracovania „dát“ v ILP procesoroch sa uskutočňuje prostredníctvom nanovlákien.
- [x] Paralelné spracovania „dát“ v ILP procesoroch sa uskutočňuje aplikovaním princípu prúdového spracovania.
- [ ] Paralelné spracovania „dát“ v ILP procesoroch sa uskutočňuje prostredníctvom výtokových slotov.

**Vysvetlenie**:
merged-pps.pdf strana 519: Časový kontra priestorový paralelizmus

|                           | Prúdové spracovanie | Zvyšovanie počtu funkčných jednotiek |
| ------------------------- | ------------------- | ------------------------------------ |
| ILP procesory             | +                   |                                      |
| VLIW procesory            | +                   | +                                    |
| Superskalárne procesory   | +                   | +                                    |

---

### ID_OTAZKY: 041
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Označte pravdivý, resp. pravdivé výroky.

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [ ] Simultánny superskalárny model je možné uplatniť v jednovláknových TLP procesoroch.
- [ ] Po cykloch prekrývaný VLIW model je možné uplatniť v jednovláknových TLP procesoroch.
- [x] Simultánny superskalárny model je možné uplatniť v multivláknových ILP procesoroch.
- [ ] Po cykloch prekrývaný superskalárny model je možné uplatniť v jednovláknových TLP procesoroch.

**Vysvetlenie**:
- **1. ✗** Simultánny multivláknový (SMT) model vyžaduje viac vlákien — *jednovláknový TLP procesor* je protirečenie.
    - merged-pps.pdf strana 577: *simultánny multivláknový model (superskalárna verzia)* — je to model pre multivláknové TLP architektúry (Obr. 8.1, strana 578)
- **2. ✗** Po cykloch prekrývaný model je inherentne multivláknový (prekladá inštrukcie z rôznych vlákien po cykloch).
    - merged-pps.pdf strana 577: *po cykloch prekrývaný model (skalárna a superskalárna verzia)* — model multivláknových TLP architektúr (Obr. 8.1, strana 578)
- **3. ✓** Simultánny superskalárny model = SMT na superskalárnej ILP architektúre; umožňuje multivláknovému ILP procesoru vykonávať inštrukcie z viacerých vlákien súčasne.
    - merged-pps.pdf strana 577: *simultánny multivláknový model (superskalárna verzia)* — model pre multivláknové TLP architektúry
    - merged-pps.pdf strana 596: *Multivláknové architektúry sú paralelné architektúry, kde sa inštrukcie vykonávajú vo vláknach skalárne, superskalárne, resp. podľa princípu VLIW*
- **4. ✗** Po cykloch prekrývaný superskalárny model je multivláknový princíp, ktorý vyžaduje viac vlákien — nedá sa uplatniť v jednovláknovom procesore.
    - merged-pps.pdf strana 577: zaradený pod multivláknové TLP architektúry (Obr. 8.1, strana 578)

---

### ID_OTAZKY: 042
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Ktoré výroky sú pravdivé?

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [x] Mikrovláknový superskalárny model je možné uplatniť v multivláknových TLP procesoroch.
- [x] Nanovláknový superskalárny model je možné uplatniť v multivláknových TLP procesoroch.
- [x] Po cykloch prekrývaný VLIW model je možné uplatniť v multivláknových ILP procesoroch.
- [x] Simultánny superskalárny model je možné uplatniť v multivláknových ILP procesoroch.

**Vysvetlenie**:
- merged-pps.pdf strana 231, 576, 598: **1. ✓** Mikrovláknový model je uvedený ako model multivláknových (TLP) architektúr. Môže mať superskalárnu verziu (blokovo prekrývaná superskalárna / simultánna superskalárna). Je uplatniteľný v TLP procesoroch.
- merged-pps.pdf strana 231, 576, 598: **2. ✓** Nanovláknový model je rovnako uvedený pod multivláknovými TLP architektúrami so superskalárnou verziou.
- merged-pps.pdf strana 516, 603: **3. ✓** VLIW je klasifikovaný ako ILP procesor (strana 516: *"Skalárne ILP procesory, Superskalárne ILP procesory, VLIW"*). Na strane 603 sú uvedené *"VLIW procesory s cyklickým prekrývaním"* a *"cyklus-za-cyklom prekladaný VLIW"* — ide o multivláknový VLIW procesor (kombinácia ILP + TLP), teda uplatniteľný v multivláknových ILP procesoroch.
- merged-pps.pdf strana 231, 576, 598: **4. ✓** Simultánny multivláknový model (superskalárna verzia) je model TLP architektúr. Superskalár je ILP technika; SMT na superskalári vytvára multivláknový ILP procesor.

---

### ID_OTAZKY: 043
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý?
Pri načítaní operandov vo fáze Odosielania (angl. Dispatch) len pamäť registrov obsahuje informáciu o platnosti obsahu príslušného zdrojového (resp. cieľového) registra.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

**Vysvetlenie**:
- merged-pps.pdf strana 559: Pri načítaní operandov vo fáze Odosielania (Dispatch) **len pamäť registrov** obsahuje informáciu o platnosti obsahu zdrojového/cieľového registra — P-zásobník túto informáciu neobsahuje.

---

## Skupina: Prepojovacie siete a manipulácia s údajmi

### ID_OTAZKY: 044
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Prepojovacia funkcia prepojovacej siete N-dimenzionálna kocka je definovaná zápisom:
$$f_i(p_{n-1} \dots p_1 p_0) = p_{n-1} \dots p_{i+1} \overline{p_i} p_{i-1} \dots p_0$$

**Otázka**:
Vyberte jednu odpoveď

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

### ID_OTAZKY: 045
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Prepojovacia funkcia prepojovacej siete **N-dimenzionálna kocka** je definovaná zápisom
$f(p_{n-1} \dots p_1 p_0) = p_0 p_{n-1} \dots p_2 p_1$

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [ ] Pravda
- [X] Nepravda

**Vysvetlenie**:
Funkcia $f(p_{n-1} \dots p_1 p_0) = p_0 p_{n-1} \dots p_2 p_1$ je definícia **inverzného premiešania (shuffle⁻¹)**, nie prepojovacej funkcie siete N-dimenzionálna kocka.

- merged-pps.pdf strana 503: Pre N-dimenzionálnu kocku je definovaná funkcia
  $$cube_i(p_{n-1} \dots p_1 p_0) = p_{n-1} \dots p_{i+1} \bar{p_i} p_{i-1} \dots p_0$$

- merged-pps.pdf strana 499: Inverzné premiešanie je definované ako
  $$shuffle^{-1}(p_{n-1}p_{n-2} \dots p_1p_0) = p_0p_{n-1} \dots p_2p_1$$

### ID_OTAZKY: 046
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Aká je adresa prijímača v prepojovacej sieti 256x256 ak
- vysielač má hexadecimálnu adresu 0x21;
- prijímače a vysielače sú spojené pomocou permutačnej siete s permutačnou funkciou dokonalé premiešanie.

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] 0x42
- [ ] 0x20
- [ ] 0x22
- [ ] 0x10

**Vysvetlenie**:
- merged-pps.pdf strana 499: Prepojovacia sieť 256×256 používa 8-bitové adresy ($256 = 2^8$). Permutačná funkcia **dokonalé premiešanie (perfect shuffle)** je definovaná ako:
$$shuffle(p_{n-1}p_{n-2} \dots p_1p_0) = p_{n-2}p_{n-3} \dots p_0p_{n-1}$$
čo zodpovedá rotácii doľava o 1 bit.

Vysielač: `0x21` = `0010 0001` (binárne, 8 bitov).
Po aplikovaní shuffle: `0100 0010` = `0x42`.

Prijímač má teda adresu **0x42**.

### ID_OTAZKY: 047
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Operácie pre manipuláciu s údajmi definované **manipulačnými funkciami (MF)**, ktoré sa rozdeľujú do tried:

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [x] Kopírovanie
- [x] Permutácie
- [x] Rozmiestnenie
- [x] Maskovanie

**Vysvetlenie**:
- merged-pps.pdf strana 511: Všetky štyri triedy sú správne. Manipulačné funkcie (MF) sa rozdeľujú do tried: **Permutácia(-e)**, **Kopírovanie**, **Rozmiestnenie** a **Maskovanie**.

---

## Skupina: Výkonnosť a škálovanie

### ID_OTAZKY: 048
**Typ**: Multiple-Choice (Select ONE or MANY)

**Kontext**:
Ktorý výrok, resp. výroky sú pravdivé ohľadom modelu MK?

**Otázka**:
Označte jednu alebo viac odpovedí:

**Odpoveď**:
- [X] Model môže byť prípadne limitovaný komunikačným ohraničením (KB).
- [ ] Korešponduje s oblasťou medzi krivkami L a E.
- [ ] Model korešponduje s lineárnym nárastom pracovnej záťaže.
- [X] Pracovná záťaž je konštantná.
- [ ] Je limitovaný pamäťovým ohraničením (MB).

**Vysvetlenie**:
- merged-pps.pdf strana 327: **Model MK** (fixed-load model): pracovná záťaž je konštantná, model môže byť prípadne limitovaný komunikačným ohraničením (KB).
- merged-pps.pdf strana 327: **Model MT** (fixed-time model): korešponduje s lineárnym nárastom pracovnej záťaže.
- merged-pps.pdf strana 327: **Model MM** (fixed-memory model): korešponduje s oblasťou medzi krivkami L a E, je limitovaný pamäťovým ohraničením (MB).

---

### ID_OTAZKY: 049
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý?
$$Speedup\ (p\ processors) = \frac{Time\ (1\ processor)}{Time\ (p\ processor)}$$

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [X] Pravda
- [ ] Nepravda

**Vysvetlenie**:
- merged-pps.pdf strana 7: Speedup je definovaný ako pomer výkonov: $Speedup(p) = \frac{Performance(p)}{Performance(1)}$. Pre fixnú veľkosť problému platí $Performance = 1/Time$, teda $Speedup(p) = \frac{1/Time(p)}{1/Time(1)} = \frac{Time(1)}{Time(p)}$, čo je presne uvedený vzorec.

---

### ID_OTAZKY: 050
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Predstavme si auto idúce z miesta A do miesta B, pričom tieto miesta sú vzdialené 60 km. Za prvú hodinu jazdy auto prešlo 30 km.
Gustafsonov zákon hovorí,

**Otázka**:
Označte jednu odpoveď:

**Odpoveď**:
- [ ] že aj keď auto absolvuje zvyšok cesty ľubovoľnou rýchlosťou, nemôže jeho priemerná rýchlosť prekročiť 60 km/h (aj keby išiel po prvej hodiny jazdy „svetelnou“ rýchlosťou, prešiel by 60 kilometrov za hodinu).
- [X] že ak auto pôjde dostatočne ďaleko, môže dosiahnuť ľubovoľnú priemernú rýchlosť. Aby napríklad dosiahlo v priemere 90 km/h, stačí, aby jazdilo ďalšiu hodinu rýchlosťou 150 km/h alebo ďalšie dve hodiny rýchlosťou 120 km/h apod.

**Vysvetlenie**:
- merged-pps.pdf strana 351: Gustafsonov zákon si volí za konštantu dobu behu na paralelnom systéme. V analógii s autom to znamená, že ak auto pôjde dostatočne ďaleko (predĺži čas), môže dosiahnuť ľubovoľnú priemernú rýchlosť. Na rozdiel od Amdahlovho zákona, ktorý fixuje veľkosť problému (60 km), Gustafsonov zákon škáluje problém — čím dlhšie auto ide, tým viac sa "rozpustí" vplyv pomalého začiatku.

---

### ID_OTAZKY: 051
**Typ**: Single-Choice (Select ONE)

**Kontext**:
Je tento výrok pravdivý ?
$$Speedup\ (p\ processors) = \frac{Performance\ (1\ processor)}{Performance\ (p\ processors)}$$

**Otázka**:
Vyberte jednu:

**Odpoveď**:
- [ ] Pravda
- [x] Nepravda

**Vysvetlenie**:
- merged-pps.pdf strana 7: $Speedup(p) = \frac{Performance(p)}{Performance(1)}$
- Pre porovnanie, v termínoch času (Time) platí $Speedup(p) = \frac{Time(1)}{Time(p)}$, keďže $Performance = 1/Time$

---
