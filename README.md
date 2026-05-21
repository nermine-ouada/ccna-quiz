# CCNA Practice

Interactive study app for **CCNA 1** and **CCNA 2**, built with [Next.js](https://nextjs.org/) 14, React, and Tailwind CSS. Questions are parsed from offline HTML answer sheets and served as flashcards or a scored quiz.

## Features

- **Flashcards** — reveal answers, shuffle the deck, optional reverse traversal
- **Quiz** — multiple choice, ordering, and match-pair questions with progress saved in the browser
- **Course picker** — CCNA 1 or CCNA 2 on the home page
- **Dark mode** — system-aware theme toggle
- **Reference pages** — static answer HTML at `/ccna1.html` and `/ccna2.html`

## Getting started

**Requirements:** Node.js 18+

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

| Script        | Description              |
|---------------|--------------------------|
| `npm run dev` | Development server       |
| `npm run build` | Production build       |
| `npm run start` | Run production build   |
| `npm run lint` | ESLint                  |
| `npm run parse` | Regenerate question JSON from HTML |

## Project layout

```
app/              # Pages (home, flashcards, quiz)
components/       # UI (questions, match pairs, theme)
data/             # questions-ccna1.json, questions-ccna2.json, answer-patches.json
lib/              # Question loading, parser, quiz persistence
public/           # Static HTML answer sheets (ccna1.html, ccna2.html)
ccna1.html        # Source HTML for the parser (CCNA 1)
ccna2.html        # Source HTML for the parser (CCNA 2)
scripts/          # Maintenance helpers for CCNA 2 HTML / JSON order
```

## Updating questions

1. Place or update `ccna1.html` and `ccna2.html` in the project root (copies are also under `public/` for browsing).
2. Run:

   ```bash
   npm run parse
   ```

   This writes `data/questions.json`, `data/questions-ccna1.json`, and `data/questions-ccna2.json`.

Manual corrections that should survive re-parsing belong in `data/answer-patches.json` (keyed by course and question id).

### CCNA 2 maintenance scripts

- `node scripts/rebuild-ccna2-html-toc.mjs` — rebuild table-of-contents anchors in `ccna2.html`
- `node scripts/reorder-ccna2-appendix.cjs` — reorder `data/questions-ccna2.json` to match the HTML appendix section

## Credits

Question content is derived from CCNA course materials. Original HTML workflow and data: [nermine-ouada/ccna2](https://github.com/nermine-ouada/ccna2).
