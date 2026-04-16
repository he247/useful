# Sparklines mit LaTeX (`sparklines`)

Sparklines sind sehr kleine, in Fließtext integrierte Datenvisualisierungen (Micro-Charts), populär gemacht durch Edward Tufte. Sie zeigen Trends auf engem Raum, ohne den Lesefluss durch große Diagramme zu unterbrechen.

## Wichtigste Element-Typen

> Die Unicode/ASCII-Demos sind nur visuelle Approximationen für GitHub Markdown, nicht das exakte Render-Ergebnis von LaTeX.

### 1) `\spark` – Liniengraph

```latex
\begin{sparkline}{10}
  \spark 0.1 0.95 0.3 0.3 0.5 0.62 0.7 0.5 1.0 0.2 /
\end{sparkline}
```

**Demo (ASCII/Unicode):** `▁█▂▂▄▅▆▄█▂`  
**Anwendungsfall:** Gut für Zeitreihen mit Fokus auf Trend und Verlauf. Beispiel: Aktienkurs, Temperaturkurve oder tägliche Umsätze.

### 2) `\sparkspike` – Balkendiagramm

```latex
\begin{sparkline}{5}
  \sparkspike .083 .18
  \sparkspike .25 .55
  \sparkspike .417 1.0
  \sparkspike .583 .62
  \sparkspike .75 .42
\end{sparkline}
```

**Demo (ASCII/Unicode):** `▂▅█▆▄`  
**Anwendungsfall:** Sinnvoll für diskrete Werte pro Intervall, z. B. Monatsbesuche oder Fehler pro Build. Spitzen sind sofort erkennbar.

### 3) `\sparkdot` – Markierungspunkte

```latex
\begin{sparkline}{10}
  \spark 0.1 0.95 0.3 0.3 0.5 0.62 0.7 0.5 1.0 0.2 /
  \sparkdot 0.25 0.62 blue
  \sparkdot 1.0 0.2 red
\end{sparkline}
```

**Demo (ASCII/Unicode):** `▁█▂●▄▅▆▄█●`  
**Anwendungsfall:** Markiert gezielt Min/Max, Ausreißer oder Schwellwertverletzungen. Hilfreich bei KPI-Reviews mit erklärungsbedürftigen Punkten.

### 4) `\sparkrectangle` – Hintergrundband

```latex
\begin{sparkline}{10}
  \sparkrectangle 0.35 0.65
  \spark 0.1 0.95 0.3 0.3 0.5 0.62 0.7 0.5 1.0 0.2 /
\end{sparkline}
```

**Demo (ASCII/Unicode):** `░░▒▒▓▓▒▒░░` (Band) + Linie  
**Anwendungsfall:** Zeigt Normal- oder Zielbereiche im Hintergrund. Nützlich, um sofort zu sehen, wann Messwerte außerhalb eines tolerierten Bereichs liegen.

### 5) Kombination: Linie + Balken + Punkte

```latex
\begin{sparkline}{10}
  \sparkspike .2 .35
  \sparkspike .4 .75
  \sparkspike .6 .45
  \spark 0.1 0.25 0.3 0.55 0.5 0.35 0.7 0.8 0.9 0.4 /
  \sparkdot 0.7 0.8 red
\end{sparkline}
```

**Demo (ASCII/Unicode):** `▃▆▄` + `▁▃▅▄▇▅` + `●`  
**Anwendungsfall:** Für kompakte Mehrfachaussagen in einem Mini-Chart: Volumen (Balken), Trend (Linie), Ereignisse (Punkte). Geeignet für Umsatz + Ausreißer in einem Satz.

### 6) `\sparkbottomline` – Grundlinie

```latex
\setlength\sparkbottomlinethickness{.2pt}
\begin{sparkline}{10}
  \sparkbottomline 0
  \spark 0.1 0.2 0.3 0.4 0.5 0.35 0.7 0.55 0.9 0.8 /
\end{sparkline}
```

**Demo (ASCII/Unicode):** `──────────` + `▂▃▄▃▅▆`  
**Anwendungsfall:** Eine klare Nulllinie verbessert die Einordnung von Wachstum/Verlust. Besonders hilfreich bei Differenzwerten um 0 oder bei Performance-Delta.

## Vergleich: Sparklines in anderen Tools

| Tool/Umgebung | Beispielansatz | Interaktivität | Geeignet für |
|---|---|---|---|
| LaTeX (`sparklines`) | Inline-Kommandos wie `\spark`, `\sparkspike`, `\sparkdot` | Nein (statisch im PDF) | Wissenschaftliche/technische Texte mit präzisem Satzbild |
| Python (`matplotlib`/`plotly`) | Mini-Achsen oder Sparkline-Funktion per Script | Mit `plotly`: Ja | Reports, Notebooks, Dashboards |
| Typst | Kleine Linien/Balken über Zeichenfunktionen/Packages | Eher statisch | Moderne, codebasierte Dokumente als LaTeX-Alternative |
| Markdown (Unicode/ASCII) | Zeichen wie `▁▂▃▄▅▆▇█` oder `|`-Balken | Nein | Sehr leichtgewichtige READMEs, Issues, Changelogs |
| R (`ggplot2`/`sparkline`) | Inline-Plots oder htmlwidgets | Teilweise (HTML) | Statistik- und BI-Workflows |
| Vega-Lite | JSON-Spezifikation für Mini-Charts | Ja (im Web) | Web-Dokumentation, eingebettete interaktive Visuals |

## Farb-, Größen- und Stil-Anpassung

- **Farbe:** Nutze konsistente Farbsemantik (z. B. Rot nur für Warnungen, Blau für neutrale Trends).
- **Größe:** Sparklines sollen klein bleiben; sie ergänzen Text und ersetzen keine Hauptgrafik.
- **Linienstärke/Punktgröße:** Nicht zu dick wählen, sonst wirkt die Sparkline wie ein normales Diagramm.
- **Kontrast:** Hintergrundband (`\sparkrectangle`) dezent halten, damit Linie und Marker lesbar bleiben.

## Typische Fehler

- Zu viele Elemente kombinieren (überladene Mikro-Grafik).
- Unterschiedliche Skalen ohne Kennzeichnung vergleichen.
- Farben ohne Bedeutung verwenden.
- Min/Max-Punkte markieren, aber im Text nicht erklären.
- In Markdown erwarten, dass Unicode-Demos die exakte LaTeX-Geometrie replizieren.
