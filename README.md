<img width="1909" height="894" alt="Screenshot 2026-03-19 085306" src="https://github.com/user-attachments/assets/1ed415d4-7214-4211-8e89-f4b64fc2ac63" />
# Header UI Prototype


Responsiver Header- und Navigations-Prototype mit modernen CSS- und HTML-Features. Gebaut mit purem HTML5, CSS3 und minimalem JavaScript – nur dort wo es wirklich nötig ist.

---

## 🌟 Das Besondere an diesem Projekt

### Native HTML Popover API – kein JavaScript für Dropdowns
Die Nav-Dropdowns nutzen die **HTML Popover API**, ein Feature das 2023/2024 in allen modernen Browsern gelandet ist und in der Praxis noch kaum eingesetzt wird. Kein JavaScript, kein CSS-Hack, keine Library – das Öffnen und Schließen übernimmt der Browser nativ über `popovertarget`.

```html
<button popovertarget="dropdown-products">Products +</button>
<div id="dropdown-products" popover class="nav-dropdown">...</div>
```

Das bedeutet: automatisches Schließen bei Klick außerhalb, native Keyboard-Navigation und Accessibility – alles ohne eine einzige Zeile JavaScript-Logik.

Minimales JS übernimmt **ausschließlich** die Positionierung direkt unter dem Button via `getBoundingClientRect()`. Logik und Positionierung sauber getrennt.

Für ältere Browser ist ein **automatischer Fallback** per Feature Detection eingebaut – das Dropdown funktioniert in jedem Browser, nutzt aber native Browser-Features wo sie verfügbar sind:

```javascript
// Progressive Enhancement: moderner Pfad vs. Fallback
const supportsPopover = HTMLElement.prototype.hasOwnProperty('popover');

if (supportsPopover) {
    // Popover API übernimmt – JS nur für Positionierung
} else {
    // Manueller Toggle für ältere Browser
}
```

Das nennt sich **Progressive Enhancement** – eine der wichtigsten Prinzipien in der professionellen Frontend-Entwicklung.

### DSGVO-konforme Self-hosted Assets – kein CDN
Font Awesome Icons sowie beide Webfonts (**Rounded Mplus 1c**, **PT Sans Caption**) sind vollständig lokal eingebunden. Keine externen Requests, keine Tracker, keine Abhängigkeit von Drittanbietern.

```css
@font-face {
    font-family: 'Rounded Mplus 1c';
    src: url('../webfonts/RoundedMplus1c-Regular.woff2') format('woff2');
    font-display: swap; /* Performance: kein Flash of Invisible Text */
}
```

`font-display: swap` sorgt zusätzlich dafür dass der Text sofort sichtbar ist während die Schrift lädt – ein häufig übersehenes Performance-Detail.

---

## 📁 Projektstruktur

```
/
├── index.html
├── css/
│   ├── stylesheet.css
│   └── fontawesome.css     ← Self-hosted, kein CDN
├── img/
│   └── logoipsum-257.png
└── webfonts/
    ├── RoundedMplus1c-*.woff2
    ├── PTSans-CaptionBold.woff2
    └── fa-*.woff2
```

---

## 🧩 Seitenaufbau

**Navigation** – Sticky Nav mit Logo, drei Dropdown-Menüs via Popover API, Pricing/Contact-Links und CTA-Button. Auf Mobile Hamburger-Menü.

**Header / Hero** – Vollflächiger Gradient-Hero mit zentrierter Überschrift, Untertitel, Trennlinie und sechs interaktiven Icon-Karten.

**Icon-Karten** – Jede Karte zeigt ein Font Awesome Icon und einen Label. Per Klick auf den `+`-Button öffnet sich ein Tooltip mit Beschreibung und Link – per CSS-Toggle, kein Popover nötig.

---

## ✨ Weitere CSS-Highlights

**CSS Custom Properties** – Alle Farben, Abstände und Styles zentral als Variablen in `:root` definiert. Änderungen an einer Stelle wirken sich auf die gesamte Seite aus.

**Fluid Typography** – Überschriften skalieren stufenlos mit `clamp()`, keine abrupten Sprünge durch Media Query Breakpoints.

```css
--font-h1-size: clamp(2rem, 5vw, 3rem);
```

**Karten-Tooltips per CSS-Toggle** – Die Info-Tooltips auf den Karten nutzen `opacity` + `pointer-events` + `transform` für eine saubere Ein-/Ausblend-Animation. JS setzt nur eine Klasse, CSS macht den Rest.

```css
.card-tooltip          { opacity: 0; pointer-events: none; }
.card.is-open .card-tooltip { opacity: 1; pointer-events: auto; }
```

**`prefers-reduced-motion`** – Alle Animationen werden für Nutzer deaktiviert die das in den Systemeinstellungen bevorzugen.

---

## 📱 Responsive Breakpoints

| Breakpoint | Änderungen |
|---|---|
| `≥ 1280px` | Padding auf 10vw |
| `≥ 1700px` | Padding auf 20vw |
| `≤ 900px` | Hamburger-Menü, Desktop-Nav ausgeblendet, Mobile-Menü mit allen Links |
| `≤ 600px` | Karten 2-spaltig per CSS Grid |
| `≤ 380px` | Karten einspaltiger |

---

## 🛠️ Technologien

- **HTML5** – Popover API (`popovertarget`, `popover`), semantisches Markup
- **CSS3** – Custom Properties, `clamp()`, Flexbox, `position: sticky`, `pointer-events`, Transitions, `prefers-reduced-motion`
- **JavaScript** – minimal, nur Dropdown-Positionierung + Tooltip-Toggle per Klassenname
- **Self-hosted** – Font Awesome, Rounded Mplus 1c, PT Sans Caption via `@font-face` mit `font-display: swap`

---

## 📌 Browser-Support

Die Popover API wird unterstützt ab Chrome 114+, Safari 17+ und Firefox 125+. Dank **Progressive Enhancement** mit Feature Detection funktionieren die Nav-Dropdowns in allen modernen Browsern – ältere Browser erhalten automatisch eine gleichwertige JS-Fallback-Lösung mit identischem Verhalten.
