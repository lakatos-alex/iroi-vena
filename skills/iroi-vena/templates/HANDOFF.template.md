---
schema_version: "1.0"
session_id: "YYYY-MM-DD-run-01"
story_title: "A Történet Címe"
current_chapter: 1
canonical_date: "1924-11-04"
canonical_time: "08:30"
referenced_prior_chapters:
  - chapter: "Ch-00 (Előzmény)"
    reason: "Közvetlen cselekményfolytatás és időrendi indulópont"
  - chapter: "Ch-XX (Korábbi mérföldkő)"
    reason: "Itt történt a kulcsfontosságú tárgy átadása vagy a tegezési/magázási megállapodás"
  - chapter: "Ch-YY (Korábbi nyitott szál)"
    reason: "A ma érvényesülő ígéret vagy fizikai állapot eredete"
location: "Helyszín pontos megnevezése (pl. Kikötői raktárnegyed, 4-es móló)"
active_characters:
  - name: "Főszereplő 1"
    status: "Egészséges, fázik, enyhe alváshiány"
    held_items: ["vámraktári kulcscsomó", "sárgaréz zseblámpa"]
  - name: "Szereplő 2"
    status: "Éber, figyel, távolságtartó"
    held_items: ["fekete fedeles füzet", "grafitceruza"]
open_threads:
  - id: "THREAD-01"
    summary: "A hajnali vonattal érkezett lepecsételt láda felbontása"
    severity: "HIGH"
  - id: "THREAD-02"
    summary: "Eltérés a fuvarlevél sorszámában"
    severity: "MEDIUM"
next_3_actions:
  1: "Átkelni az ipari vágányon a B raktár felé a kapuőr figyelmének felkeltése nélkül."
  2: "Megkeresni a 402-es rekeszt és összevetni a plombszámot a fuvarlevéllel."
  3: "Tisztázni a szolgálatvezetővel a vontatóhajó késésének okát."
invariant_constraints:
  - "Sűrű ónos eső esik, a látótávolság legfeljebb negyven lépés."
  - "A szereplők harmadik személy jelenlétében szigorúan magázódnak (Ön)."
last_updated: "2026-09-18T00:00:00Z"
---

# Aktív Narratív Állapot (Active Narrative State)

## 1. Környezet és Fizikai Súrlódás (Scene Setting & Physical Friction)
- **Helyszín és hőmérséklet:** Pontos fizikai tér, huzat, fűtöttség foka, páratartalom.
- **Akusztika és szagok:** Kénes szénfüst, eső kopogása a bádogtetőn, tompa gépzúgás.
- **Tárgyi akadályok:** Beragadt retesz, átázott bakancs, csúszós macskakő, kihűlő kályha.

## 2. Aktív Feszültség és Dramaturgiai Cél (Active Plot Friction & Objective)
- **Közvetlen cél:** Mit akar a fókuszkarakter elérni ebben a szobában / jelenetben?
- **Közvetlen tét:** Mi vész el azonnal, ha hibázik vagy habozik?
- **Ellenállás:** Ki vagy mi nehezíti meg a feladatot (másik szereplő eltérő érdeke, időkorlát, fizikai sérülés)?

## 3. Episztemikus Eltérések és Titkok (Epistemic Divergence & Secrets)
- **A szereplő tudja:** [Pl. A raktárkulcs másolata a zsebében van.]
- **B szereplő hiszi (tévesen):** [Pl. Úgy tudja, a kulcs az irodában maradt a széfben.]
- **Az Olvasó tudja:** [Pl. A kulcs nála van, de a széfet már feltörték.]

## 4. Fizikai Tárgybirtoklási Nyilvántartás (Physical Custody Register)
- **Kritikus tárgy 1:** Kinél van, melyik zsebben / táskában, milyen állapotban?
- **Kritikus tárgy 2:** Hol lett letéve, ki látta meg utoljára?
