# Írói Véna (`iroi-vena`)

> **Kézműves magyar prózatechnika, dramaturgia és AI-natív perzisztens emlékezet regényíróknak.**
> Készítette: **Lakatos Alex** · [lakatosalex.hu](https://lakatosalex.hu)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Skills.sh](https://img.shields.io/badge/skills.sh-iroi--vena-blue.svg)](https://skills.sh)

---

## A történet: Miért született meg ez a műhely?

Az AI pocsékul ír. Legalábbis ha magára hagyod.

Aki próbált már regényt, fejezetet vagy akár csak egy hosszabb párbeszédet íratni vele magyarul, pontosan ismeri a tüneteket:
- **Az anglicizmusok és tükörfordítások fogsága:** A mondatok nem magyarul lélegeznek. Minden bekezdésben ott kísért az elhagyhatatlan alany (*„Ő odalépett, és ő ránézett”*), a modoros körülírások (*„a lány”, „a férfi”, „az előbbi”*), és a passzív, nyakatekert szerkezetek.
- **A kényszeres szentimentalizmus:** A szereplők folyamatosan tikkelnek (*felsóhajtanak, bólintanak, összehúzzák a szemöldöküket*), a narrátor pedig képtelen megállni a cselekvésnél: minden mozdulat után elmagyarázza, mit kell érezni, és a jelenet végén didaktikus kiselőadást tart a szerelem, a remény és az emberi lélek nagyságáról.
- **A memóriasodródás (Context Drift):** A harmadik fejezetre az AI elfelejti a tegnap szerzett sebeket, a kimondott titkokat, és ha két szereplő összevész, három bekezdés múlva reflexből kibékíti őket, megölve minden valódi feszültséget.

Ez a projekt nem elméleti laborban született. Saját, efemer csevegésekből indult: írni akartam, de a modellek folyamatosan elcsúsztak. Ekkor kezdtem el „projectifikálni” az egészet: Git-verziókezelés, fejezetműhely, Markdown-alapú történetbibliák, tudásháló-nyilvántartás és szigorú negatív kényszerek. Hosszú, több százezer leírt és átszerkesztett szóból álló regényfolyamok és szerializált történetek során a módszertan lassan hógolyóvá nőtte ki magát.

Az **Írói Véna** ennek a kísérletnek a letisztult, általánosított, nyílt forráskódú gyümölcse: **a legmagasabb szintű magyar irodalmi kézművesség és az AI-natív perzisztens emlékezet ötvözete**.

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

---

## Telepítés

### A hivatalos `skills` CLI segítségével:

```bash
# Telepítés Cursor, Codex vagy Claude Code alá:
npx skills add lakatos-alex/iroi-vena --skill iroi-vena
```

### Manuális integráció:
Másold be a könyvtárat a projekted `.cursor/skills/iroi-vena/` vagy `.agents/skills/iroi-vena/` mappájába.

---

## A Modulok Felépítése

| Fájl | Témakör |
| :--- | :--- |
| **[SKILL.md](SKILL.md)** | A központi router, negatív kényszerek és a 4-fázisú munkafolyamat (English-pivoted). |
| **[persistent-memory.md](references/persistent-memory.md)** | Kétszintű perzisztens memóriaprotokoll, YAML-séma, anti-belief-inertia (angol specifikáció). |
| **[hungarian-prose.md](references/hungarian-prose.md)** | Topik–fókusz mondattan, igekötők, névmástakarékosság, mélyérzékelés. |
| **[hungarian-typography.md](references/hungarian-typography.md)** | Párbeszéd-gondolatjelek, aszimmetrikus megszólítások, SMS és cset-formátum. |
| **[scene-craft.md](references/scene-craft.md)** | Fizikai súrlódás a jelenetben, jelenet vs. összefoglalás, gesztusinfláció irtása. |
| **[character-and-trust.md](references/character-and-trust.md)** | A bizalom 4 rétege, gondoskodás mint munka vs. kontroll, határok védelme. |
| **[continuity-and-knowledge.md](references/continuity-and-knowledge.md)** | Az 5 tudásállapot, tárgybirtoklás, kötelezettségek és ígéretek kezelése. |
| **[genre-profiles.md](references/genre-profiles.md)** | Műfaji profilok: Kortárs realista, Krimi/Noir, Sci-fi/Fantasy, Történelmi. |
| **[evals/cases.md](evals/cases.md)** | Minőségi értékelési szempontrendszer és valós vakteszt esettanulmány. |
| **[evals/harness_plan.md](evals/harness_plan.md)** | A tervezett automatikus helyi tesztkörnyezet (Eval Harness) architektúrája és esetei. |

---

## Licenc és Szerzőség

Készítette: **Lakatos Alex** ([lakatosalex.hu](https://lakatosalex.hu))
Licenc: **MIT License**. Szabadon használható, beépíthető és továbbfejleszthető mind egyéni írói projektekben, mind kereskedelmi rendszerekben.
