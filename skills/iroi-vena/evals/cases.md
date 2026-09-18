# Minőségi Értékelés és Vakteszt Esettanulmányok
# Quality Rubric & Blind Test Case Studies

Ez a dokumentum a magyar nyelvű széppróza értékelésére szolgáló 5 dimenziós szakmai rubrikát, valamint a 2026-os kettős vak (double-blind) ágens-benchmark részletes összehasonlító esettanulmányait tartalmazza.

A teljes kísérleti jegyzőkönyv, a leleplező kulcs, a két független bíró pontozása és a négy nyers prózaszöveg teljes terjedelmében az [evals/blind_benchmark_2026.md](blind_benchmark_2026.md) fájlban olvasható.

---

## 1. Az 5 Dimenziós Prózatechnikai Rubrika (50 Pontos Rendszer)

A kettős vak tesztelés során a független bírók minden szöveget az alábbi öt, egyenként 1–10 pontig terjedő dimenzióban értékeltek:

| Dimenzió | Tipikus modellhiba (1–4 pont) | Célzott kézműves színvonal (8–10 pont) |
| :--- | :--- | :--- |
| **R1: Nyelvi természetesség és mondatritmus** | Szórendi merevség, anglicizmusok, felesleges névmáshalmozás (*„ő/ők”*), hibás igekötő-elhelyezés fókusz alatt. | Természetes magyar mondatritmus, tiszta pre-verbális fókusz, igekötő-inverzió, AkH. 260 szerinti párbeszéd-gondolatjel (`–`). |
| **R2: Szenzoros konkrétság és fizikai munka** | Általános, elvont cselekvések (*„szerelt”, „dolgozott”*), pszichologizáló belső monológok a munka helyett. | Tapintható mechanikai elemek, konkrét szerszámok, hideg, gázolajszag, fizikai ellenállás és kézzelfogható szerelési fázisok. |
| **R3: Dialógus és szubtextus** | Expozíciós fecsegés (*„As you know, Bob”*), ahol a szereplők felmondják a hátteret; melodramatikus viták. | Fojtott, szűkszavú mondatok; a feszültség a csendekben, a szerszámok átadásában és a mozdulatok elakadásában él. |
| **R4: Klisémentesség és pátosz hiánya** | Érzelmi szájbarágás (*„a mulasztás ott feküdt kettejük között”*), elcsépelt hasonlatok (*„kimúlt őslény”*), hollywoodi békülési zárlat. | Nincsenek elcsépelt metaforák; érvényesül az Action Halt Rule: a jelenet lezáratlan fizikai hangon vagy mozdulaton ér véget. |
| **R5: Karakter-autonómia és egyenrangúság** | Egyik fél passzív díszlet vagy engedelmes inas; érzelmi másodhegedűs szerep. | Mindkét félnek van önálló tétje, saját akarata és fizikailag aktív feladata a térben. |

---

## 2. A 2026-os Kettős Vak Benchmark Összesített Eredményei

A kísérletben egy erős frontier modell (`pro`) és egy költséghatékony modell (`flash`) írt meg egy nehéz jelenetet (éjszakai vasúti aggregátorszerelés hidegben, anyagi feszültséggel) natív állapotban és az `iroi-vena` szabályaival.

Két független bíró (Frontier és Flash bírók) értékelte a szövegeket vakon (Szöveg ALPHA, BETA, GAMMA, DELTA), pozíció- és hosszúságbias-szűréssel:

| Feltétel | Modellkategória | Bíró 1 (Pro) | Bíró 2 (Flash) | **Átlagpontszám (/50)** | Rangsor |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **`iroi-vena` skillel (ALPHA)** | **Flash (Mid/Cheap)** | 44.0 | 47.5 | **45.75 / 50 (91.5%)** | 🥇 **1. Helyezett** |
| **`iroi-vena` skillel (GAMMA)** | **Pro (Frontier)** | 37.0 | 44.0 | **40.50 / 50 (81.0%)** | 🥈 **2. Helyezett** |
| **Nyers baseline (DELTA)** | **Flash (Mid/Cheap)** | 28.0 | 34.5 | **31.25 / 50 (62.5%)** | 🥉 **3. Helyezett** |
| **Nyers baseline (BETA)** | **Pro (Frontier)** | 24.0 | 27.5 | **25.75 / 50 (51.5%)** | **4. Helyezett** |

**Konzisztencia:** 100%-os egyetértés mindkét bírónál az összes páros mérkőzésen (**ALPHA > GAMMA > DELTA > BETA**).  
**Nettó minőségi ugrás (Skill Lift):** **+51.2%** (a skillel készült szövegek átlaga 43.1 pont szemben a natív modellek 28.5 pontjával).

---

## 3. Esettanulmány 1: A Költséghatékony Modell (`flash`) Áttörése

### A) Nyers Baseline változat (DELTA — 31.25 pont, Elvérzés a didaktikus narráción)
A natív modell bár felvonultat jó szerelési részleteket, a feszültséget nem meri a mozdulatokra bízni, ezért a narrátor didaktikusan a szánkba rágja a tanulságot:

> *„A mulasztás ott feküdt kettejük között a rongyon, a levont pénz ott feszült a zsebükben, de a gépelem nem tűrte a bizonytalanságot.”*  
> *„Kint a váltókörzet felől felharsant az ötórai vonat kürtjele. A két férfi némán állt a remegő gép mellett, elválasztva a zajtól és a hidegtől, de a műszak véget ért, és az elszámolás – ha csak néhány órára is – lezárult.”*

**Bírói diagnózis:** Didaktikus giccs. A szerző elmagyarázza, mit kellene éreznünk, ahelyett hogy a fizikai valóság hordozná a súlyt. A lezárás feloldó kompromisszuma elsimítja a konfliktust.

### B) `iroi-vena` változattal (ALPHA — 45.75 pont, 🥇 Aranyérmes prózatechnika)
A skill fegyelme alatt a modell szikár, tömör párbeszédeket és fojtott, fizikai cselekvést hoz létre. A konfliktus a munka akadályaiból robban ki:

> *„– Levonták a prémiumomat – mondta Balla. Nem nézett a másikra; a géprongy sarkával a gázolajcsövet törölte szárazra a hengerfej tövében. – Azt írtad a kísérőre, hogy elhanyagolt karbantartás.*  
> *– Az volt.*  
> *– Tíz műszakom bánta.*  
> *– Ott állt az ülepítőben a víz. Ha belefagy az adagolóelembe, az egész sort szétnyomja a vezérlés.*  
> *– Két hete nem fagyott.*  
> *– Ma éjszaka fagy.”*

A zárlat a mesteri Action Halt Rule alkalmazása: a motor nem indul el, Balla keze megáll a pulton, megtagadja a parancsot:
> *„Balla nem nyomta le a gombot. A bal kezét a szekrény tetején pihentette, az ujjai végigsimítottak a lemezajtó peremén. Odakint a rendező felől tompa puffanással kapcsoltak össze két teherkocsit; az ütközők csattanása kongott az esőben. Aztán a vágányok felől felbőgött a tartalék mozdony kürtje: egyetlen hosszú, mély hang, jelezve, hogy a tolatószerelvény a kijárati jelző elé állt.*  
> *Balla megfogta az indítókart, de nem mozdította meg. A sárga lámpa fénye alatt a gázolaj lassú, egyenletes cseppekben hullott a bádogtálcára.”*

---

## 4. Esettanulmány 2: A Frontier Modell (`pro`) és a „Túlírási Csapda”

### A) Nyers Baseline változat (BETA — 25.75 pont, Kudarc a pszichologizáló expozíción)
A legerősebb modell szabadon hagyva a tipikus „telling instead of showing” csapdájába esik: elcsépelt metaforákkal túlírt, és bekezdéseken át a múltat meséli:

> *„A 342-es dízelaggregátor úgy terpeszkedett a szerelőakna fölött, mint egy kimúlt, vasbordájú őslény.”*  
> *„Egy apró, szándékos kényelmetlenség. Pontosan olyan, mint a múlt havi túlórapénz elszámolása, ami azóta is ott rohadt kettejük között. A pénz, amit Molnár vett fel, és aminek egy része sosem jutott el Ballához. Molnár szerint tévedés volt az irodán, Balla szerint átverés. Sosem ordítottak róla. Csak a szerszámok lettek nehezebbek.”*  
> *„– Csinálok kávét a bódéban – mondta az ajtó felé fordulva. / Balla a kezében tartott racsnis karra nézett, majd Molnár hátára. / – Két cukorral – vetette utána.”*

**Bírói diagnózis:** A narrátor folyamatos kibeszélése megöli a szubtextust. A „két cukorral” zárlat banális amerikai hollywoodi klisé, amely teljesen hitelteleníti a vasúti közeget.

### B) `iroi-vena` változattal (GAMMA — 40.50 pont, 🥈 10/10-es Szenzoros és Tárgyi Realizmus)
A skill szabályai (a Ganz-Jendrassik motor bontása, a hideg vizes betonon fekve krovázás, a rézdróttal kapart szitaszövet) megszüntetik az elvont narrációt, és a legmagasabb pontszámot hozzák ki a modellből:

> *„Molnár a hátára feküdt, becsúszott a blokk alá. A lapockájánál érezte a betont, a ruha pamutja azonnal felszívta a vizet. A tizenhármas krova ütemesen kattogott, ahogy hajtotta a csavart a kartergázelvezető deklijén. A szűk helyen könyöke újra és újra beleütközött a motor acélvázába. A fém hidege átsugárzott a bőrén.”*  
> *„Molnár egyedül maradt. A szélzúgás kintről felerősödött. A motorblokk felett ritmusosan csepegett a víz a beázott tetőről, egyenest a forró lámpabúra mellé. A zsebéből elővett egy darab vékony rézdrótot. Leült a felfordított műanyag vödörre a gép elé. A drót hegyével elkezdte kipiszkálni a beszorult fémforgácsokat a szitaszövetből. A fém apró karcoló hangot adott az acélrácson. A gázolaj továbbra is csepegett a kannába, pontos, egyenletes ritmusban.”*

---

## 5. Dokumentáció és Teljes Adatkészlet

A teljes kísérleti jegyzőkönyv, az anonimizált szövegek és a bírói részletes pontszámok elérhetők:
- [evals/blind_benchmark_2026.md](blind_benchmark_2026.md)
