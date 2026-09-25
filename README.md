# Prompt Engineering – Cheat Sheet

## Lektion 1 – Was ist Prompt Engineering

**Kernideen**

- Prompt Engineering = Prompts bewusst designen, damit LLMs verlässliche, nützliche Antworten liefern.
- Gute Prompts haben 3 Bausteine:
  - **Rolle** (wer ist das Modell?)
  - **Kontext** (in welchem Setting arbeitet es?)
  - **Output-Format** (wie soll die Antwort aussehen?)
- Bessere Prompts ⇒ bessere Qualität, weniger Halluzinationen, weniger Trial & Error.

**Merkformel**

> Rolle + Kontext + Output-Format

---

## Lektion 2 – Prompting Techniken

**Techniken**

- **Zero-Shot**
  - Keine Beispiele, nur Anweisung.
  - Einsatz: einfache, bekannte Tasks (Übersetzen, leichte Umformung, kurze Erklärungen).

- **Few-Shot**
  - Du gibst **Beispiele** vor (Input → gewünschter Output).
  - Einsatz: eigenes Schema / Format, Labels, interne Klassifikationen.

- **Chain-of-Thought**
  - Modell soll **Schritte / Gedankengang** explizit machen.
  - Einsatz: mehrstufiges Denken, Root-Cause-Analysen, komplexe Entscheidungen.

**Merksatz**

- Few-Shot = **Beispiele geben**  
- Chain-of-Thought = **Schritte zeigen lassen**

---

## Lektion 3 – Prompt-Formatierung und Struktur

**Struktur im Prompt**

- Klar trennen:
  - **Anweisung** (was das Modell tun soll)
  - **Kontext** (Hintergrund, System, Business-Kontext)
  - **Input** (Logs, SQL, Beschreibungen, Text)
  - **Output-Vorgabe** (Form, Länge, Zielgruppe)

**Wichtige Elemente**

- **Labels / Sections**:
  - Beispiel:
    - `Kontext:`
    - `Aufgabe:`
    - `Input:`
    - `Output-Format:`

- **Delimiter**:
  - Klare Start-/End-Markierung von Input-Blöcken.
  - Modell erkennt Bereiche sauberer und hält Format besser ein.

**Effekt**

- Antworten werden:
  - klarer,
  - konsistenter,
  - format-treuer.

---

## Lektion 4 – Reduzierung von Halluzinationen mit Prompting

**Grounding**

- Kontext explizit mitgeben:
  - Logs, Doku, Schema, Config, Tickets, etc.
- Dazu sagen:
  - „Antworte nur basierend auf diesem Kontext …“

**Citations**

- Antworten prüfbar machen:
  - „Zitiere relevante Stellen aus der Doku / den Logs wörtlich als Beleg.“
  - „Füge nach jeder Aussage die passende Textstelle an.“

**Scope begrenzen**

- Thema und Umfang einschränken:
  - „Nur diese Tabelle …“
  - „Nur dieses Log-Snippet …“
  - „Maximal 3 Punkte / maximal 5 Sätze …“

**Unsicherheit erlauben**

- Anweisung:
  - „Wenn Informationen fehlen, erfinde nichts.“
  - „Sage explizit, dass du es nicht sicher sagen kannst.“
  - „Formuliere Vermutungen als Hypothesen.“

**Risiko-Erkennung**

- Hohe Hallu-Gefahr bei:
  - sehr vagen Fragen,
  - extrem breiten Fragen ohne Kontext,
  - sehr spezifischen Fragen zu Systemen, deren Doku nicht gegeben ist.

---

## Lektion 5 – Iterieren und Debugging von Prompts

**Debugging-Mindset**

- Bei schlechter Antwort:
  - nicht „Modell ist schlecht“,
  - sondern zuerst: „Mein Prompt ist noch nicht klar genug.“

**Typische Prompt-Bugs**

1. **Mehrdeutig**
   - Unklare Aufgabe („Analysiere das“, „Fasse zusammen“).
   - Keine Zielgruppe, kein Fokus, keine Längenangabe.

2. **Kontext fehlt**
   - Kein Tech-Stack, keine Logs, keine Ziele, kein Business-Kontext.

3. **Widersprüchlich**
   - „Antworte kurz, aber extrem detailliert.“
   - „Für Senior Engineers und Management gleichzeitig.“

**Iterationszyklus**

1. Prompt ausführen (**Test**).
2. Antwort beobachten:
   - Was genau ist schlecht? (zu allgemein, Thema verfehlt, Format ignoriert, halluziniert …)
3. Vermutete Ursache im Prompt:
   - Mehrdeutig?
   - Kontext fehlt?
   - Widersprüchlich?
4. **Gezielt** 1–2 Dinge ändern:
   - Ziel präzisieren,
   - Kontext ergänzen,
   - Zielgruppe klar setzen,
   - Output-Format schärfen.
5. Neu testen und ggf. wiederholen.

**AI als Prompt-Reviewer**

- Meta-Prompt-Beispiel:

  „Hier ist mein Prompt: `<DEIN PROMPT>`.  
  Analysiere ihn und sag mir:  
  1. Wo ist er mehrdeutig?  
  2. Wo fehlt Kontext?  
  3. Gibt es widersprüchliche Anforderungen?  
  Mach 1–2 konkrete Verbesserungsvorschläge mit kurzer Begründung.“

- Wichtiger Punkt:
  - Vorschläge sind **Hypothesen**, die du testest, keine Wahrheit.
