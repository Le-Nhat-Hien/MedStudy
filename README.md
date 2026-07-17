# MedStudy — Bilingual Medical Lecture Platform

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Google Gemini](https://img.shields.io/badge/Gemini-8B5CF6?style=for-the-badge&logo=googleai&logoColor=white)

> A standalone, single-file bilingual (English / Tieng Viet) medical study platform powered by Google Gemini AI. No build tools, no frameworks — just open `index.html` in your browser.

---

## Demo

![Dashboard](https://img.shields.io/badge/Dark%20Mode-UI-blue?style=flat-square)

- Open `index.html` in any modern browser
- Navigate via the sidebar: **Book > Unit > Chapter > Section**
- Toggle sections open/collapse like Windows File Explorer

---

## Features

### Core Content

| Feature | Description |
|---------|-------------|
| **Bilingual Content** | Every section is presented in both English and Vietnamese side-by-side |
| **Hierarchical Navigation** | Library organized as Book > Unit > Chapter > Section with collapsible sidebar |
| **Pre-built Content** | Campbell Biology Unit 1 (Chapters 2-4): Atoms & Molecules, Water, Carbon — 17 sections with full bilingual lecture content |
| **Clinical Relevance** | Each section includes medical/clinical context boxes connecting chemistry to medicine |

### Study Tools

| Feature | Description |
|---------|-------------|
| **Question Bank** | 15+ pre-built bilingual MCQ questions filterable by chapter and difficulty (Basic / Intermediate / Advanced) |
| **Flashcards** | Flip-card study mode with question on front, answer + explanation on back |
| **Score Tracking** | Submit all answers at once to see your percentage score with color-coded feedback |

### AI-Powered (Google Gemini)

| Feature | Description |
|---------|-------------|
| **AI Question Generator** | Generate custom bilingual MCQ questions on any medical topic |
| **AI Lecture Generator** | Generate structured bilingual lecture notes from a topic or imported document |
| **Import with AI** | Import `.md` / `.txt` files and auto-generate structured bilingual content + questions via Gemini |
| **Teaching Assistant** | Floating AI chat widget that answers questions using course content as context |

### Data Management

| Feature | Description |
|---------|-------------|
| **Multiple API Keys** | Add, remove, and switch between multiple Gemini API keys with one active key |
| **Export / Import Backup** | Full data backup as JSON (questions, imports, API keys) |
| **Local Storage Persistence** | API keys and imported documents persist across sessions |
| **Import System** | Drag-and-drop or manual import of `.md` / `.txt` files with optional AI processing |

---

## Architecture

Single-file architecture — the entire application lives in one `index.html` file (~110 KB):

```
index.html
├── <style>     — All CSS (~190 rules, CSS custom properties theming)
├── <body>      — HTML shell (sidebar + main content + TA chat panel)
└── <script>    — All JavaScript
    ├── DATA    — Book/Unit/Chapter/Section hierarchy + Question Bank
    ├── UI      — buildSidebar, nav, toggleSB, tSec
    ├── STUDY   — Quiz (rQuiz, subQ, resQ), Flashcards (rFlash, flip)
    ├── AI      — genContent, Gemini API integration, prompt engineering
    ├── IMPORT  — processImport, file handling, AI-enhanced import
    ├── TA      — Teaching Assistant chat (sendTAMessage, context builder)
    └── CONFIG  — API key management, export/import data, localStorage
```

### Data Model

```javascript
BOOKS = [{ id, name, icon }]        // Top-level: books (Campbell, future books...)
U = [{ id, n, t, tv, ic, ch: [     // Units within books
  { id, t, tv, sec: [               // Chapters within units
    { id, t, tv, en, vi }           // Sections (bilingual content)
  ]}
]}]
QB = [{ id, u, ch, s, tp, df,       // Question Bank
        q, qv, o, ex, exv }]
S = { pg, imp, fi, ff,              // Application state
      keys, activeKey, expNav }
```

### Navigation State

Sidebar expand/collapse state is tracked in `S.expNav`:
- `b:campbell` — book level
- `u:unit-1` — unit level
- `c:unit-1:ch2` — chapter level

Uses the same `tSec()` toggle pattern as the main content section headers.

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari)
- A Google Gemini API key (free tier available)

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/medstudy.git
   ```
2. Open `index.html` in your browser
3. Go to **Settings** and add your Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)
4. Start studying!

### Adding More Books

To add content from other textbooks, modify the `BOOKS` array and `U` array in the `<script>` section:

```javascript
var BOOKS = [
  { id: 'campbell', name: 'Campbell Biology', icon: 'fas fa-dna' },
  { id: 'guyton', name: 'Guyton Physiology', icon: 'fas fa-heartbeat' }
];
```

Or use the **Import** page to add `.md` / `.txt` files with optional AI processing.

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **HTML5** | Semantic structure |
| **CSS3** | Custom properties theming, responsive grid, dark mode UI |
| **Vanilla JavaScript** | Zero dependencies, SPA routing, state management |
| **Font Awesome 6** | Icon library |
| **Google Fonts (Inter)** | Typography |
| **Google Gemini API** | AI content generation and chat |

---

## UI Design

- **Dark mode** with blue/indigo accent gradient
- **File Explorer-style** sidebar with collapsible tree navigation
- **Responsive** — adapts to mobile screens
- **Card-based** layout for units, questions, and documents
- **Color-coded** difficulty tags (Basic / Intermediate / Advanced)
- **Bilingual badges** (EN / VI) for content sections

---

## License

This project is for educational and personal study use.

---

*Built for medical students who study across languages.*
