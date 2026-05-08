# 🎮 Roblox Coding School

> Multilingual landing page for an online Roblox Studio coding school for children aged 6–15. Built with vanilla HTML, CSS, and JavaScript — no frameworks needed.

**[Live Demo →](https://your-username.github.io/robloxkool)**

---

## ✨ Features

- **3 languages** — Estonian (default), Russian, English with instant switching, no page reload
- **Persistent language** — choice saved to `localStorage`, restored on revisit
- **Fully responsive** — mobile-first, tested from 320px to 1440px
- **Smart enrolment form** — auto-recommends a course level based on child's age and experience
- **Form validation** — inline error messages in the active language
- **Tabbed course sections** — 3 age groups (6–8, 9–11, 12–15) with animated transitions
- **FAQ accordion** — rebuilt dynamically on language change
- **Dark premium design** — Inter font, CSS custom properties, smooth hover states

---

## 🛠 Tech Stack

| Layer   | Choice                          | Why                        |
| ------- | ------------------------------- | -------------------------- |
| Markup  | HTML5 semantic                  | Accessibility + SEO        |
| Styling | Vanilla CSS + Custom Properties | No build step, fast load   |
| Logic   | Vanilla JS (ES6)                | Zero dependencies          |
| Font    | Inter (Google Fonts)            | Consistent across ET/RU/EN |
| Deploy  | GitHub Pages / Vercel           | Free, instant CI/CD        |

---

## 🌍 i18n Architecture

All UI strings live in a single `translations` object in `script.js`:

```js
const T = {
  et: { hero_h1: "Sinu laps loob päris mänge...", ... },
  ru: { hero_h1: "Твой ребёнок создаёт...", ... },
  en: { hero_h1: "Your child creates real games...", ... }
}
```

HTML elements are tagged with `data-i18n="key"` attributes. A single `applyLang(lang)` function walks the DOM and swaps all text at once — no flicker, no layout shift.

```html
<h1 data-i18n="hero_h1">Sinu laps loob päris mänge</h1>
```

```js
function applyLang(lang) {
  document.querySelectorAll("[data-i18n]").forEach((el) => {
    const key = el.getAttribute("data-i18n");
    if (T[lang][key]) el.textContent = T[lang][key];
  });
  localStorage.setItem("rk_lang", lang);
}
```

---

## 📋 Form Logic

The enrolment form recommends a course automatically based on two inputs:

```js
function calcCourse(age, level) {
  if (level === "experienced" || age >= 12) return "lv3"; // Studio Pro
  if (age >= 9) return "lv2"; // Game Creator
  return "lv1"; // World Builder
}
```

Validation messages are pulled from the active language object, so errors always appear in the user's chosen language.

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/robloxkool.git
cd robloxkool
```

No build step needed — open `index.html` directly in a browser, or use Live Server in VS Code.

```
📁 robloxkool/
├── index.html     # Structure + i18n data attributes
├── styles.css     # Design system, layout, responsive
├── script.js      # Translations, form logic, FAQ builder
└── img/           # Dark-background images (PNG)
```

---

## 🎨 Design Decisions

**Why no framework?** The client required a single deployable file for GitHub Pages with no build pipeline. Vanilla JS with `data-i18n` attributes achieves full i18n without React/Vue overhead.

**Why Inter?** Cyrillic (RU) and Latin (ET/EN) both render cleanly at all weights. Syne — the original choice — stretched awkwardly at heavy weights in Russian.

**Why CSS custom properties?** The three course levels (teal / indigo / amber) share identical card components. CSS variables let one component cover all three states without duplication.

---

## 📬 Contact

Built by [Your Name](https://github.com/your-username) · [LinkedIn](https://linkedin.com/in/your-profile)
