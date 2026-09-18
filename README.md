# Írói Véna (`iroi-vena`)

Magyar próza írásához, átdolgozásához és hosszabb történetek folytonosságának követéséhez készült ágens-skill. Mondatvezetési, párbeszéd- és jelenetépítési útmutatókat, valamint történetbiblia- és átadási sablonokat tartalmaz.

Készítette: **Lakatos Alex** · [lakatosalex.hu](https://lakatosalex.hu) · [MIT licenc](LICENSE)

## Miért készült?

Saját regényírás közben két visszatérő problémával találkoztam: a modellek magyar szövegében sok volt a modoros fordulat, néhány fejezet után pedig elvesztek a korábban rögzített részletek. Külön fájlokba gyűjtöttem a kánont, követni kezdtem a szereplők állapotát, és írástechnikai szabályokat adtam az ágensnek. Az Írói Véna ezekből a tapasztalatokból nőtt ki.

## Mit tartalmaz?

- **Magyar mondatvezetés:** topik és fókusz, igekötők helye, névmáshasználat, mondatritmus és érzéki részletek.
- **Párbeszéd:** magyar központozás, tegezés és magázás, módosítószók, beszélőváltás, SMS és cset megjelenítése.
- **Jelenetépítés:** szereplői célok, a környezetből adódó akadályok, jelenet és összefoglalás váltása, a túlmagyarázott érzelmek és ismétlődő gesztusok visszafogása.
- **Karakterek és kapcsolatok:** önálló döntések, személyes határok, a bizalom négy dimenziója és a jóvátétel következményei.
- **Folytonosság:** ki mit tud, kinél van egy tárgy, mely sérülések, ígéretek és kötelezettségek vannak még érvényben.
- **Műfaji útmutatók:** kortárs realista próza, krimi és noir, sci-fi és fantasy, történelmi történetek.

Az egyik központi szabály az „Állj meg a cselekvésnél” (Action Halt Rule): ha egy mozdulat már hordozza a jelenet érzelmi jelentését, ne kövesse azt magyarázó tanulság. A skill több visszatérő fordulatot kifejezetten tilt, és a tárgyi részletekre épülő, visszafogott elbeszélést részesíti előnyben.

A belépési pont a [skills/iroi-vena/SKILL.md](skills/iroi-vena/SKILL.md). Az ágens innen választja ki és olvassa be a feladathoz szükséges referenciákat. Az utasítások nagyrészt angolul íródtak, magyar példákkal; a készülő próza nyelve magyar.

A csomag Markdown-útmutatókból, sablonokból és leíró metaadatokból áll. A memóriafájlok létrehozását, olvasását és frissítését az ágens végzi az utasítások alapján. Ezekhez nincs külön futó szolgáltatás vagy automatikus ellenőrző program a verziókezelt csomagban.

## Előfeltételek

A használathoz szükséges:

- Olyan AI-ágens, amely be tudja olvasni a `skills/iroi-vena/SKILL.md` fájlt és a hivatkozott modulokat, és képes magyar szöveggel dolgozni.
- A történetállapot fájlos kezeléséhez olvasási és írási hozzáférés a saját regényprojektedhez.
- A választott ágenshez szükséges modellhozzáférés. A projekt nem ír elő konkrét szolgáltatót vagy modellt, és saját API-kulcsot sem kezel.

A parancssori telepítéshez Node.js, npm és az `npx` parancs, Git, valamint a csomag és a repó letöltéséhez hálózati hozzáférés kell. A repó nem rögzít minimális Node.js-verziót; a telepítő követelményeit a [skills CLI dokumentációja](https://github.com/vercel-labs/skills) tartalmazza.

Kézi bemásoláshoz nincs szükség Node.js-re. A skill használata nem igényel Pythont, adatbázist vagy buildlépést. A saját kézirat Git-verziókezelése választható.

## Telepítés

Hozz létre külön munkakönyvtárat a regénynek, és abban telepítsd a skillt:

```bash
mkdir a-hollok-varosa
cd a-hollok-varosa
npx skills add lakatos-alex/iroi-vena --skill iroi-vena
```

A telepítőben válaszd ki az általad használt ágenst és a projekt szintű telepítést. A skills CLI többek között a Cursor, a Codex és a Claude Code telepítési helyeit is kezeli.
A repó a szabványos `skills/iroi-vena/` konténerstruktúrát használja, így a telepítő automatikusan felismeri a skillt, és a teljes moduláris referenciakönyvtárral (`references/`), valamint sablonjaival (`templates/`) együtt csomagolja, kizárva a fejlesztési és tesztelési metaadatokat.

Kézi telepítésnél másold a `skills/iroi-vena/` mappa tartalmát (`SKILL.md`, `references/` és `templates/`) az ágens által olvasott skillkönyvtárba, a belső mappaszerkezet megtartásával. A projektben leírt helyek például `.agents/skills/iroi-vena/` és `.cursor/skills/iroi-vena/`; a megfelelő helyet az ágens határozza meg.

A regény fejezeteit és állapotfájljait a saját munkakönyvtáradban tartsd, a skill telepítési mappáján kívül. Így a skill és a kézirat külön frissíthető.

## Használat és történetállapot

A regényprojektben kérd az ágenstől az `iroi-vena` skill használatát. Add meg a történet alaphelyzetét, műfaját, szereplőit és az aktuális feladatot; meglévő kéziratnál jelöld meg a mérvadó fájlokat is.

A skill négy munkaszakaszt ír elő:

1. **Előkészítés:** a történetállapot és a szükséges referenciák beolvasása, a jelenet céljának és korlátainak tisztázása.
2. **Írás:** magyar mondatvezetés, a szereplők döntéseire és a helyzet konkrét részleteire épülő próza.
3. **Átdolgozás:** ok-okozat és folytonosság, nyelv és stílus, majd tipográfia ellenőrzése.
4. **Átadás:** az aktuális állapot mentése, szükség esetén a kánon frissítése, a következő lépések rögzítése.

Az alapértelmezett memóriahely a regényprojekt `docs/` mappája:

| Fájl | Tartalom és frissítés |
| :--- | :--- |
| `docs/STORY_BIBLE.md` | Világszabályok, karakterek, kapcsolatok és szereplői tudás. Új kánontény vagy jelentős változás esetén frissül. |
| `docs/HANDOFF.md` | Aktuális fejezet, történetbeli idő, helyszín, szereplők állapota, náluk lévő tárgyak és a következő három lépés. A történetet továbbvivő munka végén frissül. |

Hiányzó fájloknál az ágens a [történetbiblia](skills/iroi-vena/templates/STORY_BIBLE.template.md) és az [átadási jegyzet](skills/iroi-vena/templates/HANDOFF.template.md) sablonjából indul. A sablonok mintaneveit, dátumait és eseményeit a saját történeted adataival kell kitölteni.

A `HANDOFF.md` YAML-fejlécet használ. A memóriaprotokoll 1000 szó alatti aktív jegyzetet céloz meg; 1200 szó fölött tömörítést és a lezárt előzmények `docs/EDITORIAL_LOG.md` fájlba helyezését írja elő. A megváltozott korábbi állapotokat `[SUPERSEDED]` jelöléssel különíti el az érvényes tényektől.

A [memóriaprotokoll](skills/iroi-vena/references/persistent-memory.md) külső könyvtár használatát is leírja az `IROIVENA_MEMORY_DIR` környezeti változóval vagy a projekt gyökerében lévő `.iroi-vena.json` fájl `memory_dir` mezőjével. Ezt is az ágensnek kell értelmeznie; külön konfigurációbetöltő nincs a csomagban.

A fájlok mentését és tartalmát érdemes minden fejezet után ellenőrizni. A leírt munkafolyamat követése a használt ágens és modell szabálykövetésétől függ.

## Értékelés és tesztelés

Az [evals/cases.md](evals/cases.md) hat szempontú, összesen 12 pontos értékelési táblázatot és összehasonlító prózapéldákat tartalmaz. A szempontok a mondatvezetést, az alanykezelést, az érzéki részleteket, az elbeszélői visszafogottságot, a párbeszédet és a tipográfiát vizsgálják.

Az 1928-as kazánházi példához a dokumentum 4/12 és 12/12 pontot közöl. A különbség az adott pontozásban 8 pont. Az ebből számolt 200%-os relatív növekedés nem tekinthető az irodalmi minőség általános javulási arányának. A verziókezelt anyag nem tartalmazza a megismétléshez szükséges teljes modell-, generálási és értékelési naplót.

Az [evals/harness_plan.md](evals/harness_plan.md) a Promptfoo és az ACES használatára épülő tesztelési tervet írja le, többek között kánon-visszakeresési, állapotfrissítési és fájlmegőrzési esetekkel. A benne szereplő futtatási leírások helyi környezetre vonatkoznak: a `promptfooconfig.yaml`, az `aces/` és a futási eredmények ki vannak zárva a verziókezelésből. **Friss klónozásból a leírt tesztparancsok nem futtathatók a hiányzó fájlok pótlása nélkül.**

A helyi `aces/aces_runner.py` előre elkészült szövegeket pontoz szólistákkal és reguláris kifejezésekkel. Nem hív modellt, és önmagában nem végez élő párosított vaktesztet. A helyi Promptfoo-konfiguráció szintén kész szövegeken ellenőriz feltételeket. Ezek a szűrők egyes szabálysértések jelzésére használhatók; az értelmezést és az irodalmi szerkesztést nem fedik le.

## Fájlok

| Fájl vagy mappa | Szerep |
| :--- | :--- |
| [skills/iroi-vena/SKILL.md](skills/iroi-vena/SKILL.md) | Belépési pont, modulválasztás, közös szabályok és munkafolyamat. |
| [skill.json](skill.json), [package.json](package.json) | Név, verzió, licenc és csomagleíró adatok. A `package.json` nem definiál függőségeket vagy futtatási parancsokat. |
| [skills/iroi-vena/templates/HANDOFF.template.md](skills/iroi-vena/templates/HANDOFF.template.md) | Az aktuális történetállapot sablonja. |
| [skills/iroi-vena/templates/STORY_BIBLE.template.md](skills/iroi-vena/templates/STORY_BIBLE.template.md) | Világ-, karakter-, kapcsolat- és kánonnyilvántartás. |
| [skills/iroi-vena/references/persistent-memory.md](skills/iroi-vena/references/persistent-memory.md) | Memóriahelyek, állapotséma, frissítés és archiválás. |
| [skills/iroi-vena/references/hungarian-prose.md](skills/iroi-vena/references/hungarian-prose.md) | Magyar mondatvezetés, nézőpont, ritmus és érzéki részletek. |
| [skills/iroi-vena/references/hungarian-typography.md](skills/iroi-vena/references/hungarian-typography.md) | Párbeszéd-központozás, megszólítások és névragozás. |
| [skills/iroi-vena/references/scene-craft.md](skills/iroi-vena/references/scene-craft.md) | Jelenetépítés, tempó, környezet és szereplői önállóság. |
| [skills/iroi-vena/references/character-and-trust.md](skills/iroi-vena/references/character-and-trust.md) | Karaktercélok, határok és bizalmi viszonyok. |
| [skills/iroi-vena/references/continuity-and-knowledge.md](skills/iroi-vena/references/continuity-and-knowledge.md) | Tudás, tárgyak, sérülések és kötelezettségek követése. |
| [skills/iroi-vena/references/genre-profiles.md](skills/iroi-vena/references/genre-profiles.md) | Műfaji szempontok és magyar példák. |
| [evals/cases.md](evals/cases.md) | Értékelési szempontok és prózapéldák. |
| [evals/harness_plan.md](evals/harness_plan.md) | A helyi tesztkörnyezet terve és dokumentált esetei. |
| [ACKNOWLEDGMENTS.md](ACKNOWLEDGMENTS.md) | Források és köszönetnyilvánítás. |

## Fejlesztés és licenc

A skill útmutatóinak, sablonjainak vagy értékelési módszerének módosításához klónozd a repót:

```bash
git clone https://github.com/lakatos-alex/iroi-vena.git
cd iroi-vena
```

A verziókezelt csomaghoz nincs buildlépés vagy mellékelt automatikus tesztfuttató. Módosításkor ellenőrizd a relatív hivatkozásokat, a sablonok és a memóriaséma összhangját, valamint azt, hogy a példák megfelelnek-e a leírt szabályoknak.

A projekt [MIT licenc](LICENSE) alatt használható és továbbfejleszthető. A felhasznált szakmai forrásokat és inspirációkat az [ACKNOWLEDGMENTS.md](ACKNOWLEDGMENTS.md) sorolja fel.
