# Írói Véna (`iroi-vena`)

> **Kézműves magyar prózatechnika, dramaturgia és AI-natív perzisztens emlékezet regényíróknak.**
> Készítette: **Lakatos Alex** · [lakatosalex.hu](https://lakatosalex.hu)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Skills.sh](https://img.shields.io/badge/skills.sh-iroi--vena-blue.svg)](https://skills.sh)

---

## A történet: Miért született meg ez a project?

Az AI pocsékul ír. Legalábbis ha magára hagyod.

Aki próbált már regényt, fejezetet vagy akár csak egy hosszabb párbeszédet íratni vele magyarul, pontosan ismeri a tüneteket:
- **Az anglicizmusok és tükörfordítások fogsága:** A mondatok nem magyarul lélegeznek. Minden bekezdésben ott kísért az elhagyhatatlan alany (*„Ő odalépett, és ő ránézett”*), a modoros körülírások (*„a lány”, „a férfi”, „az előbbi”*), és a passzív, nyakatekert szerkezetek.
- **A kényszeres szentimentalizmus:** A szereplők folyamatosan tikkelnek (*felsóhajtanak, bólintanak, összehúzzák a szemöldöküket*), a narrátor pedig képtelen megállni a cselekvésnél: minden mozdulat után elmagyarázza, mit kell érezni, és a jelenet végén didaktikus kiselőadást tart a szerelem, a remény és az emberi lélek nagyságáról.
- **A memóriasodródás (Context Drift):** A harmadik fejezetre az AI elfelejti a tegnap szerzett sebeket, a kimondott titkokat, és ha két szereplő összevész, három bekezdés múlva reflexből kibékíti őket, megölve minden valódi feszültséget.

Ez a projekt nem elméleti kísérlet. Saját tapasztalatból indult: regényt akartam írni, de a sima csevegésekben a modellek pár fejezet után menthetetlenül szétcsúsztak. Ekkor kezdtem el rendszert építeni köré: Git-verziókezelést, fejezetről fejezetre átadott állapotfájlokat, a kánont rögzítő jegyzeteket és szigorú műhelyszabályokat. Több százezer leírt szó és folyamatos kísérletezés után ebből a gyakorlatból állt össze a mostani keretrendszer.

Az **Írói Véna** ezt a gyakorlatot adja közre: természetesebb magyar mondatvezetés, kevesebb AI-modorosság és megbízható memóriakezelés a fejezetek között.

---

## A két pillér és a hibrid architektúra

A legújabb kutatások és benchmarkok (NeurIPS / ACL) igazolják: még a legfejlettebb reasoning modellek belső rejtett tere (latent space) is döntően angol-centrikus. A nem-angol procedurális utasítások belső fordítási vargabetűt (translation detour) és gyengébb szabálykövetést okoznak.

Ezért az **Írói Véna** tudatos **hibrid architektúrára** épül:
- **Vezérlési és logikai réteg (English-Pivoted Control):** A memóriasémák, invariáns negatív kényszerek, állapotgépek és életciklus-kampók tiszta, szigorú angol nyelven kényszerítik ki a modell maximális fegyelmét.
- **Magyar irodalmi motor (Native Hungarian Craft):** A generált szöveg, a szintaxis (fókusz–topik, igekötő-inverzió), a dialógus-tipográfia és a mélyérzéki szókincs közvetlenül autentikus magyar nyelven lélegzik.

### 1. A Magyar Prózatechnikai Motor (Craft Engine)
Nem sablonos írói tanácsok gyűjteménye, hanem szigorú mérnöki szabályrendszer az LLM-nek:
- **Topik–fókusz szórend és igekötő-inverzió:** A magyar mondatban a hangsúlyos állítás a ragozott ige elé kerül, tagadásnál és fókusznál az igekötő kötelezően elválik.
- **Névmástakarékosság:** A személyrag azonosítja az alanyt; a harmadik személyű kétértelműséget cselekvéssel oldja fel a szöveg, nem modoros címkékkel.
- **Action Halt Rule (Állj meg a cselekvésnél!):** Ha egy mozdulat vagy átadott tárgy hordozta az érzelmet, a narráció megáll. Nincs utólagos elmagyarázás, és szigorúan tilos a bináris *„nem azért..., hanem...”* fordulat.
- **Élő magyar partikulák:** A feszültséget a módosítószók finomhangolása (`hát`, `csak`, `ugyan`, `már`, `azért`) adja a dialógusokban.
- **Mélyérzékelés (Sensory Palette):** Nem pusztán vizuális leírások, hanem taktilis súrlódás, akusztikai terek, szagok és belső testi (viszcerális) feszültség.

### 2. Kétszintű AI-Natív Perzisztens Emlékezet (Two-Tier Memory)
Elvetjük a Cline-féle monolitikus 7-fájlos Memory Bankot, amely súlyos token-adót (4-12 ezer token turnönként) és kontextus-rothadást okoz. Helyette egy fegyelmezett, kétszintű memóriamodellt használunk:
- **Tier 1 — Invariáns Kánon (`docs/STORY_BIBLE.md`):** A világ fizikai törvényei, karakterdossziék, a bizalom 4 rétege és az episztemikus tudásháló (ki mit tud / hisz tévesen).
- **Tier 2 — Dinamikus Állapot-Staféta (`docs/HANDOFF.md`):** Egyetlen szigorúan kötött terjedelmű (< 1000 szó), YAML-frontmattes átadási fájl a pillanatnyi fizikai korlátokról, birtokolt tárgyakról és a következő 3 konkrét lépésről.
- **Anti-Belief-Inertia & Invalidation:** Explicit `[SUPERSEDED]` jelölések és kötelező lezárási mentés (Memory Flush Hook) a múltbeli sebek és állapotok túlracionalizálása ellen.
- **Workspace-Izoláció és Frissítésvédelem:** A memóriafájlok (`docs/HANDOFF.md`, `docs/STORY_BIBLE.md`) kizárólag az író saját regénykönyvtárában jönnek létre az első futtatáskor a mellékelt sablonokból (`templates/*.template.md`). A skill frissítése (`npx skills update`) így garantáltan soha nem írja felül a történeted állapotát.

---

## Telepítés és Munkafolyamat (Hol írjam a regényt?)

> [!IMPORTANT]
> **Ez a repó egy ESZKÖZKÉSZLET (Skill / Motor), NEM maga a regényed könyvtára!**
> Ha klónozod ezt a repót (`git clone`), azt csak akkor tedd, ha magát az Írói Véna motort, a prózatechnikai szabályokat vagy a tesztkörnyezetet kívánod fejleszteni.
> **Soha ne ebben a repóban kezdj el regényt írni!** Ha ide írod a fejezeteidet, a későbbi `git pull origin main` parancsok vagy motorfrissítések konfliktust okozhatnak.

### A helyes regényírói munkafolyamat:

1. **Hozz létre egy saját, független projektet a könyvednek:**
   ```bash
   mkdir a-hollok-varosa
   cd a-hollok-varosa
   git init
   ```
2. **Telepítsd be az Írói Vénát skillként a regényed alá:**
   - A hivatalos `skills` CLI segítségével (Cursor, Codex, Claude Code):
     ```bash
     npx skills add lakatos-alex/iroi-vena --skill iroi-vena
     ```
   - Vagy manuálisan másold be a könyvtárat a projekted `.cursor/skills/iroi-vena/` vagy `.agents/skills/iroi-vena/` mappájába.
3. **Kezdj el dolgozni az ágenssel a saját projektedben:**
   - Az ágens az első indításkor (Bootstrap Hook) automatikusan létrehozza a `docs/HANDOFF.md` és `docs/STORY_BIBLE.md` fájlokat a regényed gyökerében a skill sablonjaiból (`templates/*.template.md`).
   - A könyved és az emlékezete a saját git verziókezelésed alatt fejlődik, miközben a skillt bármikor frissítheted anélkül, hogy a történetállapot sérülne.

---

## Minőségellenőrzés és Vaktesztek: Nem hitvita, hanem mérés

Egy írástechnikai motornál a legkönnyebb elméleti okoskodásba csúszni: mindenki azt állítja, az ő promptja ad szebb mondatokat. Mi nem bemondásra hiszünk a szabályok erejében. A szövegminőséget és a szabálykövetést két független megközelítésben, számszerűsített tesztekkel mérjük:

- **[Promptfoo](https://github.com/promptfoo/promptfoo):** Könnyűsúlyú CLI és tesztkörnyezet, amellyel determinisztikus szabályok, negatív szószűrők és metrikák mentén vizsgálható az LLM-ek szabálykövetése.
- **[ACES (Agentic Continuous Evaluation of Skills / NVIDIA SkillEvaluator)](https://github.com/NVIDIA/SkillEvaluator):** Párosított vaktesztekkel (paired live trials) számszerűsíti a „Skill Lift”-et, vagyis a skill által hozott tényleges hozzáadott értéket a nyers modellel szemben.

### A mért eredmény: +200% Skill Lift (+8,0 pont)

Egy 1928-as külvárosi kazánházi jelenetben (beragadt forró gőzszelep, megalázó kölcsönkérési szituáció) mértük össze a nyers alapmodellt az Írói Véna motorjával:
- **Nyers modell (Baseline):** Azonnal elbukott a didaktikus lezáráson (*„a remény szétáradt a szívükben”*), a gépies gesztusinfláción és a modoros névmásozáson (**4,0 / 12,0 pont**).
- **Írói Véna motor:** Szikáran megállt a fizikai mozdulatnál (Action Halt Rule), betartotta a magyar dialógus-tipográfiát, és a kézzel fogható, mélyérzéki tárgyi részletekre építette a feszültséget (**12,0 / 12,0 pont**).

Ez a szigorú vakteszten **+200,0%-os minőségi ugrást (+8,0 pont Skill Lift)** eredményezett.

A tesztek helyben, a repó gyökeréből közvetlenül futtathatók:
```bash
# 1. Determinisztikus negatív szűrők és formai linter
npx --yes promptfoo@latest eval --no-share

# 2. ACES párosított minőségi próba és Skill Lift riport
python aces/aces_runner.py
```
*(A tesztfájlok, futási naplók és generált riportok a `.gitignore` védelme alatt állnak, így egyetlen felesleges bájtot sem hagynak a forrásfában.)*

---

## A Modulok Felépítése

| Fájl / Mappa | Témakör |
| :--- | :--- |
| **[SKILL.md](SKILL.md)** | A központi router, negatív kényszerek és a 4-fázisú munkafolyamat (English-pivoted). |
| **[templates/HANDOFF.template.md](templates/HANDOFF.template.md)** | Azonnal inicializálható dinamikus staféta sablon (YAML frontmatterrel). |
| **[templates/STORY_BIBLE.template.md](templates/STORY_BIBLE.template.md)** | Kánon történetbiblia és bizalmi mátrix sablon. |
| **[persistent-memory.md](references/persistent-memory.md)** | Kétszintű perzisztens memóriaprotokoll, YAML-séma, anti-belief-inertia (angol specifikáció). |
| **[hungarian-prose.md](references/hungarian-prose.md)** | Topik–fókusz mondattan, igekötők, névmástakarékosság, mélyérzékelés. |
| **[hungarian-typography.md](references/hungarian-typography.md)** | Párbeszéd-gondolatjelek, aszimmetrikus megszólítások, SMS és cset-formátum. |
| **[scene-craft.md](references/scene-craft.md)** | Fizikai súrlódás a jelenetben, jelenet vs. összefoglalás, gesztusinfláció irtása. |
| **[character-and-trust.md](references/character-and-trust.md)** | A bizalom 4 rétege, gondoskodás mint munka vs. kontroll, határok védelme. |
| **[continuity-and-knowledge.md](references/continuity-and-knowledge.md)** | Az 5 tudásállapot, tárgybirtoklás, kötelezettségek és ígéretek kezelése. |
| **[genre-profiles.md](references/genre-profiles.md)** | Műfaji profilok: Kortárs realista, Krimi/Noir, Sci-fi/Fantasy, Történelmi. |
| **[evals/cases.md](evals/cases.md)** | Minőségi értékelési szempontrendszer és valós vakteszt esettanulmány. |
| **[evals/harness_plan.md](evals/harness_plan.md)** | Az automatikus helyi tesztkörnyezet (Promptfoo + ACES Skill Lift) architektúrája és esetei. |
| **[ACKNOWLEDGMENTS.md](ACKNOWLEDGMENTS.md)** | Szakmai források, elméleti hivatkozások és köszönetnyilvánítás. |

---

## Licenc, Források és Szerzőség

- Készítette: **Lakatos Alex** ([lakatosalex.hu](https://lakatosalex.hu))
- Licenc: **[MIT License](LICENSE)**. Szabadon használható, beépíthető és továbbfejleszthető mind egyéni írói projektekben, mind kereskedelmi rendszerekben.
- Források és köszönetnyilvánítás: A felhasznált elméleti munkák, nyelvészeti források és inspirációt nyújtó nyílt forráskódú módszertanok részletes listája az **[ACKNOWLEDGMENTS.md](ACKNOWLEDGMENTS.md)** dokumentumban található.
