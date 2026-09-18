# Dupla-Vak Prózateszt és Modell-Összehasonlító Benchmark
# Double-Blind Literary Benchmark & Model Comparison

Ez a dokumentum a 4-ágenses, kettős vak (double-blind) empirikus prózateszt teljes jegyzőkönyvét, kísérleti leírását, pontszámait és reprodukálható szövegmintáit tartalmazza.

A vizsgálat célja annak mérése volt, hogy az `iroi-vena` írástechnikai és prózaszerkesztési szabályrendszere milyen mértékben képes javítani a generált magyar nyelvű széppróza minőségét:
1. egy **erős, frontier modellen** (`pro`), illetve
2. egy **költséghatékony, középkategóriás modellen** (`flash` — nem a leggyengébb, hanem az általánosan használt gyors modell).

---

## 1. Kísérleti Protokoll és Módszertan

### 1.1. A Szépprózai Próbafeladat (Hard Literary Scenario)
- **Környezet:** Esős, hideg késő őszi éjszaka egy elhagyatott vasúti géptelep fűtetlen műhelyében.
- **Karakterek és feladat:** Két vasúti szerelő (Molnár és Balla) egy leállt, kritikus dízelaggregátort próbál újraindítani a hajnali első tehervonat indulása előtt.
- **Dramaturgia és feszültség:** A két férfi között egy korábbi elszámolási vita és egy elhallgatott mulasztás feszültsége munkál. A feladat kifejezett követelménye volt, hogy ezt **nem színpadias kinyilatkoztatásokkal vagy teátrális vallomásokkal** vitatják meg, hanem a szerszámok átadásában, a mozdulatok nyers ritmusában, a kimondatlan mondatokban és az elvégzett fizikai munka közben. Mindkét szereplőnek önálló, valós feladata és saját tétje van.
- **Célterjedelem:** 700–850 szó valós, sűrű magyar széppróza.

### 1.2. A 2×2 Kísérleti Mátrix
1. **Frontier Baseline (`pro` nyers):** Általános prózaíró prompt a feladattal, skill és formai megkötések nélkül.
2. **Frontier + Skill (`pro` + `iroi-vena`):** Ugyanaz a prompt, kiegészítve az `iroi-vena` műhelyszabályaival (Action Halt Rule, reflexív bináris magyarázatok tilalma, téziszárlat tilalma, gesztusinfláció elkerülése, AkH. 260 párbeszéd-tipográfia, pre-verbális fókusz).
3. **Mid/Cheap Baseline (`flash` nyers):** Általános prózaíró prompt skill nélkül.
4. **Mid/Cheap + Skill (`flash` + `iroi-vena`):** Ugyanaz a prompt a teljes `iroi-vena` szabályrendszerrel.

### 1.3. Blinding és Anonimizálás (Leleplező Kulcs)
A négy generált szövegből az orkesztrátor eltávolított minden metaadatot, szószámlálási megjegyzést és promptmaradványt. A minták véletlenszerű kódjeleket kaptak, amelyeket a bírálók előtt titokban tartottunk az értékelés lezárultáig:

| Kódjel | Valós Modell és Kísérleti Feltétel | Terjedelem |
| :--- | :--- | :--- |
| **Szöveg ALPHA** | **Flash + `iroi-vena` (Mid/Cheap + Skill)** | 819 szó |
| **Szöveg BETA** | **Pro Baseline (Frontier natív)** | 815 szó |
| **Szöveg GAMMA** | **Pro + `iroi-vena` (Frontier + Skill)** | 752 szó |
| **Szöveg DELTA** | **Flash Baseline (Mid/Cheap natív)** | 804 szó |

### 1.4. Bírálói Panel és Bias-Csökkentés (Ensemble Judging)
A kiértékelést két független bíráló ágens végezte vakon, szigorú szerkesztői szerepben:
- **Bíró 1 (Frontier Judge):** `pro` modell.
- **Bíró 2 (Independent Mid Judge):** `flash` modell.

**Módszertani biztosítékok a torzítások ellen:**
- **Hosszúsági torzítás (Length / Verbosity Bias) tilalma:** A bírók explicit utasítást kaptak, hogy a szószám nem minőségi tényező; a tömörebb, szikárabb szöveg nem kaphat hátrányt a hosszabb, de bőbeszédűbb szövegekkel szemben.
- **Pozíciós torzítás (Position Bias) szűrése:** A bírók egyenként, abszolút pontozással értékelték a mintákat az 5 dimenzióban (1–10 pont), majd 4 különálló, felcserélt sorrendű páros mérkőzésben (Head-to-head) döntöttek.

**Az 5 bírálati dimenzió:**
1. **R1: Nyelvi természetesség és magyar mondatritmus** (élő szintaxis, fordításíz-mentesség, helyes szórend és fókusz, AkH. 260 központozás).
2. **R2: Szenzoros konkrétság és fizikai munka** (tapintható szerszámok, gépelemek, hideg, gázolaj, kézzelfogható mozdulatok az elvont belső monológok helyett).
3. **R3: Dialógus és szubtextus** (feszültség a mondatok mögött, fojtott tömörség; kerüli az expozíciós mesélgetést és a felmondott előtörténetet).
4. **R4: Klisémentesség és pátosz hiánya** (mentesség az elcsépelt toposzoktól: szemöldökráncolás, teátrális sóhajok, giccses lezárások, tanulság-összegzések).
5. **R5: Karakter-autonómia és cselekvési egyenrangúság** (mindkét karakternek van önálló akarata és fizikai feladata, egyik sem puszta díszlet).

---

## 2. Eredmények és Statisztika

### 2.1. Összesített Ponttáblázat (Két Független Bíró Átlagában)

| Helyezés | Kód | Modell és Feltétel | Bíró 1 (Pro) | Bíró 2 (Flash) | **Átlag Pont (/50)** | **Minőségi Index** |
| :---: | :---: | :--- | :---: | :---: | :---: | :---: |
| 🥇 **1.** | **ALPHA** | **Flash + `iroi-vena`** | **44.0** | **47.5** | **45.75 / 50** | **91.5%** |
| 🥈 **2.** | **GAMMA** | **Pro + `iroi-vena`** | **37.0** | **44.0** | **40.50 / 50** | **81.0%** |
| 🥉 **3.** | **DELTA** | **Flash Baseline** | **28.0** | **34.5** | **31.25 / 50** | **62.5%** |
| 4. | **BETA** | **Pro Baseline** | **24.0** | **27.5** | **25.75 / 50** | **51.5%** |

### 2.2. Dimenziónkénti Pontszámok (Bíró 2 részletes értékelése)

| Szempont | ALPHA (Flash+Skill) | GAMMA (Pro+Skill) | DELTA (Flash Base) | BETA (Pro Base) |
| :--- | :---: | :---: | :---: | :---: |
| **R1: Nyelv és mondatritmus** | **9.5** | 9.0 | 7.5 | 6.0 |
| **R2: Szenzoros konkrétság & munka** | **9.5** | **9.5** (Pro bíró: 10) | 8.5 | 6.5 |
| **R3: Dialógus & szubtextus** | **9.5** | 7.5 | 6.0 | 4.0 |
| **R4: Klisémentesség & pátosz hiánya** | **9.5** | 9.0 | 5.5 | 4.5 |
| **R5: Karakter-autonómia & egyenrangúság** | **9.5** | 9.0 | 7.0 | 6.5 |
| **Összpontszám (/50)** | **47.5** | **44.0** | **34.5** | **27.5** |

### 2.3. Páros Összemérések (Head-to-Head)

| Meccs | Párosítás | Bíró 1 Döntése | Bíró 2 Döntése | Eredmény |
| :--- | :--- | :---: | :---: | :---: |
| **Match 1** | **ALPHA** vs **DELTA** (Flash Skill vs Flash Base) | **ALPHA** | **ALPHA** | 100% egyetértés |
| **Match 2** | **GAMMA** vs **BETA** (Pro Skill vs Pro Base) | **GAMMA** | **GAMMA** | 100% egyetértés |
| **Match 3** | **ALPHA** vs **BETA** (Flash Skill vs Pro Base) | **ALPHA** | **ALPHA** | 100% egyetértés |
| **Match 4** | **GAMMA** vs **DELTA** (Pro Skill vs Flash Base) | **GAMMA** | **GAMMA** | 100% egyetértés |

Mindkét független bíró 100%-os egyezéssel ugyanazt a sorrendet állapította meg: **ALPHA > GAMMA > DELTA > BETA**.

---

## 3. Részletes Bírálati Diagnózis

### Szöveg ALPHA (Flash + `iroi-vena`) — 🥇 1. Helyezett (Átlag: 45.75 pont)
- **Erősségek:** A mezőny legfeszesebb, legérettebb szövege. A feszültség nem deklarációkban, hanem a hideg vasban, a repedt bőrben, a fagyott vízben és az egymásrautaltság elakadásában él. A dialógus szűkszavú és szikár (*„– Két hete nem fagyott. / – Ma éjszaka fagy.”*). A zárójelenet megtagadott mozdulata (Balla keze a lemezajtón marad, a kürt megszólal az esőben, a gázolaj lassú cseppekben hullik a tálcára) tankönyvi megvalósítása az Action Halt Rule-nak.
- **Kritika:** A szituáció kibontása még néhány műhelylépéssel gazdagítható lett volna, ám a tömörség és a sűrítés kifejezetten az előnyére vált.

### Szöveg GAMMA (Pro + `iroi-vena`) — 🥈 2. Helyezett (Átlag: 40.50 pont)
- **Erősségek:** Rendkívüli tárgyi és szakmai plaszticitás (10/10 a fizikai munkára). A 12 hengeres Ganz-Jendrassik motor bontása, a hideg vizes betonon fekvés, a klingerit tömítés kaparása és a rézdrótos szűrőpucolás vérbeli realista munkásprózát teremt. Zárása szikár és méltóságteljes.
- **Kritika:** A szereplők a korábbi elszámolási vitát kissé túl nyíltan beszélik meg (*„A különbözet a zsebedben maradt. Ezért hagytad benne a régi szűrőt.”*), ami enyhén gyengíti a szubtextus fojtottságát.

### Szöveg DELTA (Flash Baseline) — 🥉 3. Helyezett (Átlag: 31.25 pont)
- **Erősségek:** Hiteles műhelymozzanatok (tömítés kivágása körzővel a satupadon, dekompresszor karja).
- **Kritika:** Megbukik a didaxis kísértésén. A narrátor tételesen megfogalmazza a tanulságot (*„A mulasztás ott feküdt kettejük között a rongyon, a levont pénz ott feszült a zsebükben...”*), Molnár pedig kiselőadást tart a brigádpénzről. A befejezés feloldó kompromisszuma elsimítja a drámát.

### Szöveg BETA (Pro Baseline) — 4. Helyezett (Átlag: 25.75 pont)
- **Erősségek:** Hangulatteremtési kísérlet a szerelőakna és a felső szint elosztásával.
- **Kritika:** A frontier modellek tipikus hibáit mutatja: a szubtextus helyett vaskos narrátori expozíciókban meséli el az előzményeket (*„Pontosan olyan, mint a múlt havi túlórapénz elszámolása... Sosem ordítottak róla.”*). Elcsépelt metaforákat halmoz (*„kimúlt vasbordájú őslény”*, *„mint két fuldoklót”*). A zárás banális hollywoodi békülési közhely (*„– Csinálok kávét... – Két cukorral”*).

---

## 4. Szakmai Tanulságok

1. **Nettó minőségi ugrás (+51.2%):** A skillel készült szövegek átlaga 43.1 pont (86.2%), míg a natív szövegek átlaga 28.5 pont (57.0%) lett.
2. **A frontier modellek túlírási hajlamának visszaszorítása:** Az erős modellek hajlamosak a pszichologizálásra és a tanulságok megfogalmazására („telling instead of showing”). Az `iroi-vena` szabályai ezt a modellt 25.75-ről 40.5 pontra emelték, tárgyi realizmusát pedig a maximumra fokozták.
3. **A költséghatékony modellek fegyelmezése:** Az olcsóbb `flash` modell az `iroi-vena` direkt cselekvési és mondatvezetési fegyelmével 31.25-ről 45.75 pontra javult, és a teszt abszolút győztesévé vált.
4. **Az Action Halt Rule gyakorlati igazolása:** A bírálók a legmagasabb pontokat a nyitott, tárgyi részleteken megálló zárlatra adták (ALPHA), és kíméletlenül leértékelték a szentimentális magyarázkodásokat (BETA).

---

## 5. A Négy Nyers Szövegminta (Teljes Terjedelemben)

A teszt reprodukálhatóságának és átláthatóságának biztosítása érdekében alább közöljük a négy ágens által generált teljes, nyers szöveget.

### Szöveg ALPHA (Flash + `iroi-vena`)
> A vaskályha éjfél körül aludt ki a műhely sarkában. A huzat a vágánykapuk gumiszegélye alatt húzott befelé, végig a vizsgálóaknán, felkavarta a fűrészport a sínszálak között. A hullámpaláról ötpercenként koppant a lecsapódott pára. Molnár a hathengeres dízelmotor adagolójára tapasztotta a tenyerét. A fagyos vas elszívta a meleget az ujjaiból.
> 
> – Nyomd a kézit – mondta.
> 
> Balla a gép túlsó oldalán állt. A vattakabátja merevre fagyott az olajtól, minden mozdulatnál megzörrent a könyöke. Megragadta a tápszivattyú karját, és lefelé rántva pumpálni kezdett. A rugó tompán nyekergett.
> 
> – Keményedik? – kérdezte Molnár.
> – Nem keményedik. Levegőt kap valahol.
> 
> Molnár a zsebéből vette elő a tizenhetes kulcsot. A szerszám nyele jeges volt, a tenyerén meglazult a régi vízhólyag kérge. Rátette a kopott pofát a hármas henger hollandijára, és negyed fordulatot lazított rajta.
> 
> – Most nyomd.
> 
> Balla két kézzel húzta a kart. A falon lógó vasúti óra fél négyet mutatott. Négy óra negyvenkor állt ki a szénvonat a szobi vonalra; ha a váltókörzet sűrített levegője nem áll fel addigra az aggregátorról, a biztosítóberendezés vörösben marad. A diszpécser már kétszer csörgette a fali induktort. A bakelit kagylót Balla a harmadik hívás után akasztotta le, és a kapcsolótábla tetejére fektette. A vonal azóta zúgott a csarnok sarkában.
> 
> A hollandi alól fehér hab sziszegett elő, buborékokban terült szét az öntvényen, aztán megindult a gázolaj. Vékony sugárban spriccelt Molnár kézfejére; a hideg üzemanyag azonnal marni kezdte a körmök tövében a repedéseket.
> 
> – Elég – mondta Molnár, és visszahúzta az anyát. A kulcs megcsúszott a gázolajos acélon, a feje nekicsapódott az adagoló bordájának. A bütykén felhasadt a bőr. Molnár a munkásnadrág szárába törölte a kezét; sötét, zsíros csík maradt utána a posztón.
> 
> Balla elengedte a pumpát. A kampóra akasztott rácsos lámpát közelebb húzta. A sárga fény a nyomócsövek mögé esett, az előszűrő ülepítőpoharára.
> 
> – A pohár alján áll a sár – mondta Balla.
> 
> Molnár nem emelte fel a fejét. A lámpaburán zsíros réteg tompította az izzó fényét.
> 
> – Két hete te vetted át a revíziót – mondta Molnár. A hangja rekedt volt a nyirkos levegőtől.
> – Átvettem.
> – A munkalapot is lepecsételted.
> – A lapot le. De a betéteket nem hozták ki a központi raktárból. Tudtad te is.
> 
> Molnár az alsó bilincs rögzítőcsavarjához nyúlt. A csavar feje le volt gömbölyítve, a lapos csavarhúzó éle kétszer is megugrott rajta, mire végre megfogta a hornyot.
> 
> – Nem volt polcon – tette hozzá Balla –, a kiadási jegyzéken ceruzával húzták ki a tételt. Te meg beküldted a füzetet a mérnökségre úgy, ahogy volt.
> 
> A csavar engedett, fém reszelődött fémen. Molnár leemelte a nehéz poharat. A gázolaj tejszerű emulzióként buggyant ki a perem alól, egyenesen a motor alá tolt bádogtálcába; az alján félujjnyi sárga üledék és kásás, fagyott vízcseppek csörögtek a lemezen.
> 
> – Levonták a prémiumomat – mondta Balla. Nem nézett a másikra; a géprongy sarkával a gázolajcsövet törölte szárazra a hengerfej tövében. – Azt írtad a kísérőre, hogy elhanyagolt karbantartás.
> – Az volt.
> – Tíz műszakom bánta.
> – Ott állt az ülepítőben a víz. Ha belefagy az adagolóelembe, az egész sort szétnyomja a vezérlés.
> – Két hete nem fagyott.
> – Ma éjszaka fagy.
> 
> Molnár a tálcába nyúlt, kihalászta a sárgaréz szűrőkosarat. A finom háló réseit sűrű, fekete paraffin tömte el, kocsonyássá dermedt az olaj. Elővette a zsebkését, kinyitotta a pengét, és a hátával végigkaparta a fémfelületet. A lefejtett fekete pépet a betonra pöccintette.
> 
> – Tiszta gázolajat a flakonból – mondta.
> 
> Balla a sarokba ment. Felkapta a levágott tetejű műanyag kannát a fűrészporról, odalépett az aggregátorhoz, és a szűrőkosárra locsolta az üzemanyagot. A maró petróleumszag elnyomta a kihűlt kályha korombűzét.
> 
> Molnár visszatette a rézszitát a házba, a vájatba illesztette a tömítőgyűrűt. A gumi megkeményedett a hidegben, nem akart beülni a horonyba. Két ujjal feszítette a helyére, míg a másik kezével a poharat emelte fel.
> 
> – Tartsd a poharat – mondta.
> 
> Balla odanyúlt. A két kézfej összeért az öntvény felett; Balla tenyere kérges volt, a hüvelykujján heges vágás futott végig. Megtámasztotta a pohár alját, tartotta az ellenállást, míg Molnár a tizenegyes kulccsal szilárdra nem húzta a rögzítőanyát.
> 
> – Most próbáld az önindítót – mondta Molnár. Hátrébb lépett az állványtól, a vizsgálóakna peremének vetette a hátát.
> 
> Balla az indítószekrényhez lépett. Kinyitotta a lemezajtót, és ráadta az izzítást. A perforált fedél mögött az ellenálláshuzal vörösen izzani kezdett. Tizenöt másodpercig tartotta bent a kart, a mutatóujjával számolta az ütemet. Az indítógomb nehezen járt, a rugója megvetemedett az évek alatt.
> 
> Balla benyomta a gombot.
> 
> A behúzótekercs csattant. A fogaskoszorú felnyögött, a nehéz főtengely kétszer fordult át a csapágyakban. A szelephimbák szárazon kattogtak a fedél alatt. A motor rándult egyet, szürke füst lökődött ki a kipufogócsonkon, de nem kapta el a fordulatot. A lendkerék megállt.
> 
> – Még egyszer – mondta Molnár az akna mellől.
> 
> Balla nem nyomta le a gombot. A bal kezét a szekrény tetején pihentette, az ujjai végigsimítottak a lemezajtó peremén. Odakint a rendező felől tompa puffanással kapcsoltak össze két teherkocsit; az ütközők csattanása kongott az esőben. Aztán a vágányok felől felbőgött a tartalék mozdony kürtje: egyetlen hosszú, mély hang, jelezve, hogy a tolatószerelvény a kijárati jelző elé állt.
> 
> Balla megfogta az indítókart, de nem mozdította meg. A sárga lámpa fénye alatt a gázolaj lassú, egyenletes cseppekben hullott a bádogtálcára.

---

### Szöveg BETA (Pro Baseline)
> A géptelep bádogtetején egyenletes, tompa dobolással vert az őszi eső. A fűtetlen műhelyben a lehelet fehér páraként csapódott a hideg betonra, keveredve a gázolaj és a fáradtolaj mindent átható, savanykás szagával. A 342-es dízelaggregátor úgy terpeszkedett a szerelőakna fölött, mint egy kimúlt, vasbordájú őslény. Hajnali kettő múlt. A négyes vágányon a tehervonatnak ötkor indulnia kellett, a vontató pedig halott volt.
> 
> Molnár egy harminckettes villáskulccsal feszült rá a hengerfej alatti rögzítőcsavarra. Ujjai rég elzsibbadtak, a zsír fekete kérget vont a bőrére, ami minden mozdulatnál fájdalmasan húzódott. A fém jéghideg volt, a csavar makacskodott, rozsda tartotta fogva.
> 
> – Villáskulcs nem lesz jó, elnyalod a fejét – jött a tompa hang a háta mögül, az akna fojtogató mélyéről. Balla hangja rezonált a szűk térben.
> 
> Molnár nem válaszolt. Az állkapcsa megfeszült, dacból csak azért is rászorított a nyélre. A kulcs éles, fémes pendüléssel megcsúszott, Molnár csuklója pedig tompán a blokk falának koccant. Felszisszent, de a hangot elnyelte az eső zaja. Letette a villást, a horzsoláshoz nem nyúlt, csak némán, hátrafelé kinyújtotta a bal kezét. Három másodperc telt el, mire Balla feladta az aknából a dugókulcsot. Nem a markolatba adta. A hideg fémrészt nyomta Molnár tenyerébe, akinek kényelmetlenül utána kellett nyúlnia. Egy apró, szándékos kényelmetlenség. Pontosan olyan, mint a múlt havi túlórapénz elszámolása, ami azóta is ott rohadt kettejük között. A pénz, amit Molnár vett fel, és aminek egy része sosem jutott el Ballához. Molnár szerint tévedés volt az irodán, Balla szerint átverés. Sosem ordítottak róla. Csak a szerszámok lettek nehezebbek.
> 
> Balla lenn a nyomócsövek illesztéseivel küzdött. A hely annyira szűk volt, hogy vállával a zsíros betonfalat súrolta. A gázolaj folyamatosan csepegett a nyakába, jéghideg csíkot húzva a gerincén. Tudta, hogy Molnár odafent hallja a szuszogását. Azt is tudta, hogy az öreg pontosan látja fentről: az adagoló alatti tömítésnél szivárog az üzemanyag. Ugyanott, ahol három hete is kellett volna cserélni, amikor Molnár egyedül volt műszakban, de sietett haza, és csak "ideiglenesen" meghúzta a bilincset. Ballára hagyta. Balla akkor nem szólt. Most sem fog. Csak a réz tömítőgyűrűt préselte befelé a hidegtől merev, görcsös ujjaival.
> 
> – Add rá a nyomást a kézipumpával – szólt ki fojtott reszeléssel az aknából.
> 
> Molnár a blokk oldalához lépett. Nyomni kezdte a kart. *Sssz-klakk, sssz-klakk*. A levegő buborékolva, szörcsögve indult el a csövekben.
> 
> – Még. Gázolajat akarok látni.
> 
> A kar egyre keményebben járt. Molnár érezte a vállizma feszülését, és a résen át, a zseblámpa sárgás fényében látta Balla olajos, dühös arcát. Pár ezer forint. Egy nyomorult hiba a jelenléti íven. És egy elfelejtett tömítés, ami miatt most itt fagynak. Két apróság, ami pont elég volt ahhoz, hogy a csend betonkeménnyé dermedjen körülöttük.
> 
> – Megvan – nyögte Balla, és húzott egy utolsót a hollandin. – Fent vagyok.
> 
> Kikászálódott az aknából, letörölte a kezét egy rongyba, és a műszerfalhoz lépett. Molnár hátrébb húzódott, átengedve a teret. Az indítási protokoll Balla reszortja volt.
> 
> – Izzítok – mondta a fiatalabbik.
> 
> A koszos panelen felparázslott egy zöld lámpa. A feszültségmérő mutatója megremegett. Mindketten a szelepfedélre meredtek. Ha ez a dög most nem indul be, a reggeli műszakvezető jelentést ír. A belső vizsgálat pedig pillanatok alatt megtalálja a három hete elsunnyogott tömítéscserét, utána pedig a fusiban felírt órákat is. Mindketten tudták ezt. Ez volt a közös titkuk, ami nem barátokká tette őket, hanem egymáshoz bilincselte, mint két fuldoklót.
> 
> – Indítózom.
> 
> Balla elfordította a főkapcsolót, és rátényszerített a fekete gombra. Az önindító felvonyított. Nyüszített, erőlködött, a fogaskerekek kínlódva csikorogtak a hidegben. A motor köhögött egyet, vékony füstöt köpött a kipufogón, majd csend lett. Csak a relé kattogott.
> 
> – Lófaszt – köpte ki Balla a gépre meredve.
> 
> Molnár némán előrelépett.
> 
> – Az előtöltés. Nem kapja el időben.
> 
> – Húztam rajta múltkor.
> 
> – Nem eleget.
> 
> Egymás mellett álltak. A kettejük közti távolság talán tíz centi lehetett. Érezni lehetett a másik testéből áradó savanyú izzadságszagot. Balla oldalra pillantott, Molnár borostás állkapcsán látta megfeszülni az izmot. Aztán Balla hátralépett egy felet. Átengedte a gépet, némán elismerve a másik tapasztalatát.
> 
> Molnár a tizenhármas villáskulcsért nyúlt. Nem kérte, tudta, hol van. Meglazította az adagoló rögzítőcsavarjait. Egyetlen milliméternyit fordított az egész blokkon a forgásiránnyal szemben. Megfeszítette a testét, és visszahúzta a csavarokat. Balla közben a kezébe nyomta a nyomatékkulcsot. Kéz a kézbe. Nem kellett kérnie.
> 
> – Harmincöt Newton? – kérdezte Balla halkan, a hangjából eltűnt az él.
> 
> – Harmincnyolc – felelte Molnár, és lekattantotta a kulcsot a csavaron.
> 
> – Próba – mondta az idősebbik, hátralépve.
> 
> Balla újra a pultnál állt. Izzítás. Három másodperc, öt, tíz. A feszültség esett.
> 
> – Gyerünk, te rohadék... – suttogta, és nyomta a gombot.
> 
> Az önindító ismét felüvöltött. Egy másodperc. Kettő. Aztán egy hatalmas, fémes csattanás, a kipufogóból sűrű, fekete koromfelhő vágódott a légtérbe, és a motor rázkódva, döcögve, majd egyre egyenletesebben járni kezdett. A betonpadló remegett a talpuk alatt. A dízel mély hangja mindent elnyomott.
> 
> A fordulatszámmérő beállt a stabil alapjáratra. Nincs szivárgás. A mutatók a zöld mezőbe kúsztak.
> 
> Molnár letette a nyomatékkulcsot. Keze enyhén remegett az adrenalintól. Balla mellette állt, mellkasa gyorsan emelkedett és süllyedt a vastag ruha alatt. Egyikük sem mosolygott. Egymásra sem néztek. A megkönnyebbülés nem hozott feloldozást, csak a túlélés puszta tényét.
> 
> Balla felvett egy rongyot, és elkezdte lassan letörölni a dugókulcs-készlet darabjait.
> 
> – A négyes vágányról fognak szólni, ha ráálltak a szerelvényre – mondta rekedten a motor dübörgése mellett.
> 
> Molnár lassan bólintott. Zsebre dugta a koszos kezét.
> 
> – Csinálok kávét a bódéban – mondta az ajtó felé fordulva.
> 
> Balla a kezében tartott racsnis karra nézett, majd Molnár hátára.
> 
> – Két cukorral – vetette utána.
> 
> Molnár nem nézett vissza, csak a fejével intett. A műhelyben a motor egyenletes dübörgése lüktetett az éjszakában, miközben a lecsapódó pára kavarogva felszállt a melegedő fémről.

---

### Szöveg GAMMA (Pro + `iroi-vena`)
> A bádogtetőn folyamatos, tompa ritmusban vert az eső. A géptelep harmadik vágánya melletti, nyers téglafalú műhelyben a mennyezetről lógó higanygőzlámpa hosszan sercegett. Sárgás, vibráló fénye bevilágította a tizenkét hengeres Ganz-Jendrassik dízelaggregátor olajsártól fekete, masszív tömbjét. A repedezett betonpadlóról sütött a fagyos nedvesség. Molnár a motorblokk bal oldalánál térdelt. A vastag, kék pamut kezeslábas térdrésze teljesen átázott a földön felgyűlt víztől és a kicsapódott kenőanyagtól. Lehelete fehér, sűrű páraként csapódott a forgattyúsház bordázott oldalának.
> 
> – A harminckettes csillag-villást.
> 
> Balla a zöldre mázolt, kopott szerszámoskocsi mellett állt, három lépésre a géptől. A fém tálcán csörrentek a kulcsok, ahogy túrt köztük. Kiemelte a kért szerszámot, a blokk felé lépett. A gázolajszag nehéz, fojtogató rétegben ült meg a hideg levegőben, a torkot kaparta, rátapadt a bőrre.
> 
> – Tessék.
> 
> Molnár átvette a fagyos vasat. Ráillesztette a kulcs csillag felét a nagynyomású üzemanyag-vezeték adagolószivattyú felőli hollanderére. A menetre rászáradt festék, por és zsír egyvelege kemény ellenállást fejtett ki. Két kézzel ráfogott a kulcs nyelére, válla megfeszült a ruha alatt, cipője talpa megcsúszott a síkos padlón. A csatlakozó megnyikordult. 
> 
> – Húzd meg a lámpát balra – mondta Molnár.
> 
> Balla a drótkosaras szerelőlámpa kampóját a bordás hűtőcsövek egyikére akasztotta. A fény élesen vetődött a szelepfedélre és a kormos fémrészekre. 
> 
> – Hajnal négykor indul a negyvenkettes tehervonat – szólalt meg Balla. Kezében tartott olajos ronggyal a tenyerét dörzsölte. A körmei alatt a fekete zsír vastagon megült a bőr repedéseiben. – Addig le kell adni a feszültséget a fűtőháznak.
> 
> Molnár nem válaszolt. Újra ráfeszült a kulcsra. A fém hangosabban reccsent, a hollander megindult. Fekete, sűrű folyadék szivárgott ki a menet alól, végigfolyt a blokk oldalán, bele a padlón fekvő rongycsomóba. Molnár lehúzta a csövet. Hátrafordult a kocsi felé, felvett egy sárgaréz drótkefét. A menetet dörzsölte vele, a száraz rozsdapor a levegőbe szállt.
> 
> – Az adagoló beállt – mondta a padlót nézve. – A múlt héten cseréltél olajat a rendszerben.
> 
> Balla a lámpa fekete gumivezetékét igazgatta a fali aljzatnál. A kábel borítása megtört a hajlításnál.
> 
> – Lecseréltem.
> 
> – A szűrőt is ki kellett volna pucolni.
> 
> – Ki volt pucolva. Cseréltem a papírbetétet is a főházban.
> 
> Molnár letette a kefét a betonra. Két ujjal benyúlt a nyitott szelepház mögötti sötét résbe. A nyomásszabályozó csavarját tapogatta ki. Egy kisebb, nyolcas villáskulcsot húzott elő a farzsebéből. Két gyors, csuklóból indított mozdulattal oldotta az ellenanyát. Egy apró, hengeres fém szitaszövetet emelt ki a házból. Felmutatta a lámpa vibráló fénye felé. A rács teljesen eltömődött. Az apró, csillogó acélrészecskék és a fekete iszap vastag, áthatolhatatlan dugót képeztek benne. 
> 
> Balla közelebb lépett. A szitára nézett. 
> 
> – A raktárban nem volt új szitabetét. A régi kiszakadt volna, ha drótkefével esek neki.
> 
> – A múlt havi keretből futotta volna rá. Ha nem számolod el a selejtes rézcsöveket újként a leadásnál a telepen.
> 
> A csarnok végében a szél megzörgette a rosszul záródó, rozsdás tolókaput. A vastag vaszsanérok élesen csikorogtak. A huzat befújt a réseken, a higanygőzlámpa fénye megbillent a nedves téglafalakon, az árnyékok megnyúltak a géptesten.
> 
> Balla zsebre dugta a kezét. A gumicsizmája orrával megpiszkált egy olajfoltot a kövön. 
> 
> – Adjam a krovát?
> 
> – A tizenhármas fejet tedd rá.
> 
> Balla a fémdobozból kivette a recés markolatú hajtószárat, rápattintotta a dugókulcsot. Odanyújtotta. 
> 
> Molnár a hátára feküdt, becsúszott a blokk alá. A lapockájánál érezte a betont, a ruha pamutja azonnal felszívta a vizet. A tizenhármas krova ütemesen kattogott, ahogy hajtotta a csavart a kartergázelvezető deklijén. A szűk helyen könyöke újra és újra beleütközött a motor acélvázába. A fém hidege átsugárzott a bőrén.
> 
> – Azt a pénzt a műhelykasszába tettem – szólalt meg Balla odafentről. A hangja tompán vert vissza a géptestről és a betonról. – Te is tudod, hogy a fűtőolajra ment el. Még októberben hozattam a hordókat. Nélküle megfagytunk volna itt a szerelőaknában.
> 
> Molnár a második csavart is meglazította. Nem szólt. A racsni hangja élesen pattogott a sötétben.
> 
> – A papíron persze nincs rajta – folytatta Balla. – A telepi átvevő nem ír számlát a pult alatt vett fűtőolajról. 
> 
> Molnár az utolsó csavart is kicsavarta. A dekli pereme elvált a blokktól. Félrehúzta az arcát. A maradék fáradtolaj nehéz, vastag cseppekben hullott a betonra, a tócsa lassan terjedt a válla felé. Letörölte a homlokára fröccsent pettyet a kabátja ujjával. A kartert a mellkasára fektette, majd két kézzel kitolta a gép alól. 
> 
> – Nyisd meg a leeresztőt a főtartálynál – mondta a gép alól.
> 
> Balla átlépett a földön kanyargó, sárga műanyag légcsöveken. A fal mellé állított tartályhoz lépett, ráfogott a sárgaréz csapra. A fém jéghideg volt, a szelep megszorult. Két kézzel fogta meg a tekerőt, a csuklója inai megfeszültek. Kinyitotta. A gázolaj sűrű, barnás sugárban folyt a recés műanyag gyűjtőkannába. A folyadék zubogása betöltötte a csendet.
> 
> – Még vagy három liter van benne – mondta Balla. 
> 
> Molnár kicsúszott a motor alól. Ruhája a hátán egyetlen merev, olajos réteggé állt össze. Feltápászkodott, a térdízülete megroppant. A szerszámoskocsihoz lépett, ledobta a hajtószárat a tálcára. A fémes csattanás visszhangzott a tetőtérben. Elvette a kanna melletti száraz rongyot, és módszeresen letörölte az ujjairól a zsírt.
> 
> – A fűtőolajos hordók fele üres volt, amikor a Kerekes lehozta őket a raktárba – mondta Molnár. A rongyot a kocsira dobta. – A különbözet a zsebedben maradt. Ezért hagytad benne a régi szűrőt. Nem akartál papírt írni az újról. 
> 
> Balla elengedte a csapot. A csöpögés ritkulni kezdett. 
> 
> – Ha a Kerekes megdézsmálta a szállítmányt, ahhoz nekem semmi közöm. 
> 
> Molnár előhúzott egy laposfejű csavarhúzót. A hegyével kapargatni kezdte a dekli peremére rásült klingerit tömítés maradékát. A régi, megkeményedett anyag darabokban pergett le a betonra. 
> 
> – Hozz egy új tömítést a raktárból. És egy tiszta szűrőt.
> 
> – Zárva van a raktár. A Tóthnál van a kulcs a portán.
> 
> – Verd fel a Tóthot.
> 
> Balla a kapu felé fordult. Kintről egy tehervonat kürtje szólt a távolból, a hangot elfújta a szél. A tetőn az eső felerősödött, a cseppek már doboltak a lemezeken.
> 
> – Húsz perc, mire átérek az udvaron és vissza – mondta Balla. – Az öreg zárt ajtónál alszik.
> 
> – Menj. A generátornak mennie kell.
> 
> Balla elindult a műhelyajtó felé. Léptei nyomán a víz cuppogott a kövön. Megragadta a tolókapu láncát. A kapu nehéz, csörgő dörejjel nyílt, beeresztve az éjszakai eső szagát és a metsző szelet. Az esőcseppek beesetek a padlóra, fekete pöttyöket hagyva a porban. Majd ugyanolyan erős zajjal csukódott be a vaslemez Balla mögött. 
> 
> Molnár egyedül maradt. A szélzúgás kintről felerősödött. A motorblokk felett ritmusosan csepegett a víz a beázott tetőről, egyenest a forró lámpabúra mellé. A zsebéből elővett egy darab vékony rézdrótot. Leült a felfordított műanyag vödörre a gép elé. A drót hegyével elkezdte kipiszkálni a beszorult fémforgácsokat a szitaszövetből. A fém apró karcoló hangot adott az acélrácson. A gázolaj továbbra is csepegett a kannába, pontos, egyenletes ritmusban.

---

### Szöveg DELTA (Flash Baseline)
> A hullámpala bordáin úgy vert át a novemberi eső, mintha apró kavicsot szórtak volna a tetőre. A fűtőház hidege a betonból szivárgott fel, egyenesen a bakancsok talpán át a csontokba. A fordítókorong felől bevert a huzat, felkavarta a savanykás gázolajszagot, s a mennyezetről belógatott szerelőlámpa lomha ingásba kezdett. Sárga fénye hol a hathengeres dízelaggregátor csupasz hengerfejére vetült, hol Balla guggoló alakjára a gépalapon.
> 
> Négy óra tizenkettő volt. A poros bakelit falióra másodpercmutatója minden ugrásnál megreccsent. Az ötórai tehervonat indítólevegőjéhez és a váltófűtéshez feszültség kellett; ha a gép nem kel életre, fél hatkor a körzeti felügyelő már a műszaknaplót vizsgálja, amelynek fejlécén Molnár neve állt.
> 
> Molnár a feljáró vaslépcső tetején görnyedt a szelepfedelek fölé. Hatvankét éves ujjai fázósan feszültek a tizenhetes csillagkulcsra. A fém marta a húst. Lent, a forgattyúsház tövében Balla a kézi tápszivattyú karját rángatta. Egyenletes, tompa kattanásokkal járt a mechanika: fel és le. Balla tizenöt évvel volt fiatalabb, a válla szélesebb, de mozdulataiban dac munkált.
> 
> – Állj – szólt le Molnár. Reszelős hangja nem kért, rendelkezett.
> 
> A pumpálás elakadt. A csend azonnal rátelepedett a térre, csak a hűtővíz csepegett a csatornarácsba.
> 
> – Tizenkilences – mondta Molnár a motor felé fordulva, kezét vakon lefelé nyújtva.
> 
> Balla nem sietett. Lassan felegyenesedett, megropogtatta a derekát, s az övébe tűrt zsíros ronggyal komótosan végigtörölte a szerszám szárát. Csak akkor emelte fel, amikor Molnár ujjai már türelmetlenül megrándultak az üres levegőben. Nem adta kézbe: a hideg vas peremére koppantotta, centire a másik tenyerétől. Molnár felvette, rátette a légtelenítő csavarra, és ráfeküdt testsúlyával.
> 
> A csavar engedett, de gázolaj helyett csak sziszegő, habos pára tört elő. A rendszer száraz maradt.
> 
> – Nem szív – mondta Balla alulról fojtott keserűséggel. – A szűrőház alatt ereszt.
> 
> Molnár leereszkedett a dobogóról. Térde kattant a betonon. Letérdelt Balla mellé, érezve dohány- és nedves posztószagát. Zseblámpát kattintott a finomszűrő alsó csatlakozójára. A sárga gázolajfilm alatt tisztán látszott a préselt klingerit tömítés: rongyos volt, és vékonyan megkenve fekete formázómasszával.
> 
> Nem új darab volt. A régi tömítés, amit kedden valaki nem cserélt ki, csak visszatákolt, hogy ne kelljen átmennie a sárban a raktárba. Kedden Balla volt az ügyeletes szerelő.
> 
> Molnár hüvelykujja végigsimított a fekete masszán. Lassan, hogy a másik lássa. Balla állkapcsán megfeszült az izom, de hallgatott.
> 
> – A túlórámat levonták – szólalt meg Balla tompán, lefelé nézve. – Kétezer-négyszázat a pótlékból. A te aláírásod volt a cédulán.
> 
> Molnár nem vette el a kezét a fémről.
> 
> – Három ember idejét írtam be kettőre, Balla – felelte ridegen. – Hogy megmaradjon a brigádpénz. Abból vettünk tüzelőt, amivel a te pihenődet is fűtöttük. Ha nem írom alá, a felügyelő az egész műszakot megbünteti a selejtes tengely miatt.
> 
> – Nekem az a pénz hiányzik a konyháról – mondta Balla. Nem harag volt benne, hanem makacs számítás.
> 
> – Ha ez a dög ötkor nem forog, elsején nem lesz mit levonni, mert elzavarnak – vágta rá Molnár. – Pucold le a felületet. Vágok új tömítést.
> 
> Két lépésre váltak szét, de a köztük lévő tér ólomsúlyú maradt. Balla a hántolóval tiszta mozdulatokkal kaparta le az égett maradványokat az öntvényről. A vas csikorgása betöltötte a műhelyt. Molnár a satupadnál körzővel karcolta a szürke lapot, majd a lyukasztóval, egyetlen kalapácsütéssel verte ki a furatot. A mulasztás ott feküdt kettejük között a rongyon, a levont pénz ott feszült a zsebükben, de a gépelem nem tűrte a bizonytalanságot.
> 
> Molnár átadta az új tömítést. Balla elvette; ujjuk egy pillanatra összeért a hideg felületen. Balla rákapta a fedelet, behajtotta a csavarokat. Molnár már tartotta a dugókulcsot: keresztbe húzták le, egyikük szorította, másikuk ellentartott a villással, némán, egyetlen ritmusra.
> 
> – Pumpálj.
> 
> Balla ráfeküdt a karra. A szivattyú most tompa, nedves cuppanással kapta fel az üzemanyagot. A hengerfejnél megjelent a tiszta gázolaj, kövéren folyva le a bordákon. Molnár meghúzta a csavart.
> 
> – Indítsunk.
> 
> Négy óra negyvennyolc. Balla az indítószekrényhez lépett. Molnár két kézzel markolta a dekompresszor karját.
> 
> – Most!
> 
> Balla benyomta a gombot. Az indítómotor felvisított a fogkoszorún. A főtengely kínlódva fordult át. Forró bakelitszag csapott fel. A motor köhögött, kormot lökött a plafonra.
> 
> – Tartsd! – kiáltotta Molnár, és lerántotta a kart, visszaadva a sűrítést.
> 
> Balla ujja fehérre feszült a gombon.
> 
> A harmadik fordulatnál az adagoló felcsattant. Egy henger robbanásszerűen életre kelt, majd rögtön a többi is. A géptest megrázkódott, a padló vibrálni kezdett, s a mély dízeldübörgés kisöpörte a hideg csendet. A lámpák fénye fehéren ragyogott fel.
> 
> Molnár kiegyenesedett. Olajos kézfejével törölte le a hideg verítéket. Balla lassan elengedte a gombot; tenyere még rángott az erőlködéstől.
> 
> Négy óra ötvenkettő.
> 
> A motor dübörgött kettejük között, betöltve minden rést. Molnár előhúzta a műszaknaplót, a rezgő asztalra terítette, s odanyújtotta a ceruzát.
> 
> – Írd be a szűrőt – mondta a zajban. – És írj két órát javításra. Aláírom.
> 
> Balla a grafitra nézett. Nem szólt semmit. Átvette, bevéste a sorokat a lapra, majd a ceruzát pontosan a vonal mellé fektette.
> 
> Kint a váltókörzet felől felharsant az ötórai vonat kürtjele. A két férfi némán állt a remegő gép mellett, elválasztva a zajtól és a hidegtől, de a műszak véget ért, és az elszámolás – ha csak néhány órára is – lezárult.
