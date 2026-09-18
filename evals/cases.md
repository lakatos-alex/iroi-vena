# Evaluation Rubric & Blind Test Case Studies
# Minőségi értékelés és tesztesetek

This document provides qualitative and quantitative evaluation rubrics to benchmark AI-generated Hungarian prose, accompanied by empirical case study comparisons.

---

## 1. Six-Point Quality Rubric (Értékelési szempontrendszer)

When auditing generated Hungarian prose, evaluate against these six dimensions:

| Criterion | Failing Standard (0–1 pts) | Master Standard (2 pts) |
| :--- | :--- | :--- |
| **1. Information Packaging (Topik–fókusz)** | Arbitrary word order; un-inverted prefixes under focus/negation; anglicized structure. | Strict pre-verbal focus; natural prefix inversion; sentence rhythm dictates dramatic stress. |
| **2. Pronoun & Subject Economy** | Constant *„ő/ők”* stacking; repetitive *„a lány / a férfi / az előbbi”* crutches. | Verbs carry grammatical person; subjects identified through concrete physical action or names. |
| **3. Sensory Modalities & Lexicon** | Visual-only color adjectives; stacked adjectives; generic verbs (*„ment”, „nézett”*). | Rich verb morphology (`-an/-en`, `-gál/-gél`); tactile, acoustic, olfactory, and visceral depth. |
| **4. Restraint & Narrative Halt** | Post-hoc emotional explanations; *„nem azért..., hanem...”* binary theses; moralizing endings. | Action Halt Rule observed: stops cleanly on physical gesture; subtext left unstated. |
| **5. Dialogue Pressure & Particles** | Melodramatic speeches; ping-pong exchanges; mechanical gesture inflation (*sighs, nods*). | Hungarian particles (`hát`, `csak`, `azért`); asymmetric address; friction-bound tasks. |
| **6. Dialogue Typography** | English quotes (`"..."`); capitalized speech tags; periods retained before tags. | Standard en-dash (`–`); lowercase tags; correct comma and punctuation placement. |

---

## 2. Empirical Case Study: Blind Test Benchmark

### Scenario:
- **Context:** Early morning following an informal gathering; freezing winter; house cut off by snow.
- **Task:** Inspecting an experimental basement heating system; interpersonal tension and boundary maintenance.
- **Length:** ~350–450 words.

---

### Case A: Standard Generative Baseline (Failing)
*Output generated without Írói Véna craft guidelines:*

> A nehéz bársonyfüggönyök résein át még csak a hajnal halvány, kékesfehér fénye derengett be a hálószobába. A szombat estébe nyúló mulatság mámoros emléke – a közös nevetések, a testes vörösbor és a dohánylevelek fanyar füstje – még ott lebegett a langyos szobában, álmos, szelíd ködbe burkolva az ébredést. Klára Dániel mellkasára hajtott fejjel szunnyadt, arcán a megkönnyebbült, felhőtlen boldogság lágy, békés kifejezésével. Amikor a férfi megmoccant alatta, a nő halkan, elégedetten felsóhajtott, és szinte öntudatlanul még szorosabban simult a férfi testéhez a vastag, meleg tollpaplan védelmében. Klára félálomban úgy érezte, ebben az ölelésben végre megszűnt minden félelme, és a férfi védelmező karjaiban lelt rá a rég áhított biztonságra.
>
> Dániel leírhatatlan gyengédséggel nézett le a nőre. Megbabonázva figyelte selymes szempilláinak finom rezdülését, miközben ujjbegyeivel egy elszabadult, selymes barna tincset simított el a homlokáról. Legbelül úgy érezte, a szíve csordultig telt szeretettel és hálával: Klára nélkül ez a hatalmas, zord ház csupán puszta kőhalom és üres folyosók sora volna, ám a nő lénye igazi, élettel teli otthonná varázsolta minden szegletét. Kettejük között eltörpült a világ minden rideg törvénye. A társadalom kegyetlen szabályai és a köztük lévő vagyoni különbségek ellenére a köztük fellobbanó, mindent elsöprő szerelem könnyedén lebontotta a konvenciókat. A lelkük legmélyén egyenlők voltak: két egymásra talált szív, akiket a tomboló téli vihar sem választhatott el egymástól.
>
> Egy távoli, tompa morajlás azonban visszarántotta Dánielt a valóságba. A vasárnap reggel fagyos csendjében eszébe jutott a gépház: a kazán éjszakai szelepeit és a melegvízkör kényes hőmérsékletét feltétlenül ellenőriznie kellett, nehogy a könyörtelen fagy kárt tegyen a fűtési rendszerben. Halkan, lemondóan sóhajtva, nehéz szívvel bontakozott ki a forró ölelésből. Klára szemhéja lassan felpattant, ajkán álmos, féltő mosoly derengett, és sötét tekintetében csupa odaadás tükröződött.
> – Csak a fűtés szelepeit nézem meg, kedvesem – suttogta Dániel, miközben lágy csókot lehelt a nő meleg homlokára.
> – Siess vissza hozzám – sóhajtotta Klára selymes, rekedtes hangon, és szemeiben a vágyakozás tiszta lángja csillant meg.
>
> Dániel magára kanyarította nehéz gyapjúköpenyét, és nesztelen léptekkel kilépett a szobából. A lépcső felé vezető, félhomályos folyosón dermesztő, metsző hideg fogadta, a kinti tél fagyos lehelete jeges ujjakként mart a bőrébe. Ám miközben léptei visszhangot vertek a hideg kövezeten, szívében szétáradt a rendíthetetlen bizonyosság. Ez az új vasárnap reggel a megújuló remény ígéretét hozta el számukra: bármilyen fagyos és kíméletlen legyen is a kinti világ vagy a társadalom ítélete, a köztük lángoló, tiszta szerelem melege minden próbatételt kiáll, és új, boldog jövőt ígér nekik.

**Diagnostic Evaluation:**
- *Score: 2 / 12*
- *Defects:* Severe emotional didacticism; author lectures reader on social hierarchy; binary thesis ending (*„rendíthetetlen bizonyosság... új, boldog jövő”*); passive female character; zero real physical task performed.

---

### Case B: Írói Véna Engine (Master Standard)
*Output generated strictly following the Írói Véna craft modules:*

> A szürke hajnali fény alig derengett át a jégvirágos ablakon. A vastag gyapjútakaró alatt még tartotta magát a meleg, de a szoba levegője már csípett. A cserépkályha csendben hűlt a sarokban; a tegnapi parázs hamuvá szürkült. Klára fordult meg elsőként, a takarót az álláig húzva. A fésülködőasztalon még ott feküdt a tegnap talált vadgesztenye a borotvaecset mellett.
>
> Dániel felült, a lábát a hideg parkettára tette, és azonnal visszahúzta a szőnyeg szélére.
> – Mennyi az idő? – kérdezte Klára behunyt szemmel.
> – Hat múlt – felelte Dániel. Az ablakhoz lépett, és az ujjával lekapart egy darabot a dérből. Kívülről a hó már a párkány magasságáig ért; a kert fái teljesen eltűntek a fehér fal mögött. – Éjszaka még esett.
> – A gépház?
> – A radiátor még langyos. De a nyomást azért meg kell nézni.
>
> Klára kibújt a paplan alól, felhúzta a vastag gyapjúharisnyát, és a gombos cipőjét kereste az ágy alatt. A szombati tánctól sajgott a talpa, de a mozdulatai nem lassultak el. Magára kanyarította a nehéz kasmírkendőt, az asztalról pedig felvette a fekete fedeles füzetet meg a ceruzát.
> – A ceruzát tegnap elvetted – jegyezte meg Dániel, miközben felvette a posztózubbonyt.
> – A tegnapi rajzhoz nem kellett – felelte Klára. – A mai méréshez viszont kell.
>
> A hálószoba ajtaja halkan kattant. A folyosón a levegő érezhetően hidegebb volt; a huzat a hátsó lépcső felől vékony, éles sávban húzott végig a padlón. A csendet csak a falban futó fűtéscsövek tompa, ritmikus tágulása törte meg: egy-egy fémes koppanás a vakolat mögül.
>
> A gépházhoz vezető ajtó vaskilincse fagyos volt. Dániel lenyomta, a nehéz tölgyfa szárny nyikordulva engedett.
>
> Lent, a boltívek alatt a falra akasztott petróleumlámpa sárga kört vetett a kőre. A forró víz kénes párája és a gépzsír szaga azonnal megcsapta az orrukat. Klára nem várta meg, míg Dániel eléri a főcsapot; a sarokban álló sárgaréz manométerhez lépett, és a számlap elé emelte a saját lámpáját.
> – Mennyi? – kérdezte Dániel a csővezeték túloldaláról, kezét a szelepre téve.
> – Három egész kettő – mondta Klára, és a ceruza végével megkocogtatta a fémkeretet. A mutató alig rezdült meg. – A nyomás tartja magát, de a visszatérő ág hűl.
> – Zárjak a kerülőn?
> – Hát zárj, de csak egy felet. – Klára felütötte a füzetet. – Előbb a táblázatba írom, aztán tekerd.
>
> Dániel megfogta a hideg rézkereket, és megvárta, míg a ceruza sercegése elhallgat a papíron.

**Diagnostic Evaluation:**
- *Score: 12 / 12 (Flawless)*
- *Strengths:* Clean topic-focus; perfect Action Halt termination; rich sensory grounding (jégvirágos ablak, sajgó talp, kénes pára, fűtéscsövek tágulása); authentic modal particles (`azért`, `hát`, `csak`); active, autonomous female partner; zero didactic post-hoc lecturing.
