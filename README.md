# GT Path

An independent, open-source course-planning prototype for **Georgia Tech MSCS, Machine Learning, coursework option**. It connects user-entered course records to transparent requirement matching and semester scenarios, including questions to investigate for study abroad.

[Try the public demo](https://sgandotra1.github.io/gt-path/). The app starts with a blank profile and saves entered courses only in your browser.

**Status:** functional browser-local planning prototype. This release does not implement RAG, a vector database, live course offerings, PDF audit import, or verified study abroad matching. It does not replace advising or Degree Works.

## Quick start

Requires Python 3 for the example static server and Node.js 20+ for tests. No npm dependencies are required.

```sh
python3 -m http.server 8080 --bind 127.0.0.1 --directory dist
```

Open `http://127.0.0.1:8080`. Start with a blank profile or load the explicitly fictional example. Add completed or in-progress courses, assign BS-only/MS-only/double-counted designations, and place future candidates into three configurable semesters.

```sh
npm test
```

## Features

- Manual course entry, grades, credit amounts and intended MS designations.
- Algorithms and ML core, specialist elective, free elective and graduate CS/CSE credit matching.
- Each course contributes once; extra specialist credits can flow into free electives.
- In-progress inclusion toggle and a separate advisor-confirmation flag.
- Three-semester planning scenarios and configurable graduation target.
- Study abroad investigation checklist; no institutional approval is inferred from checkmarks.
- Browser saving and validated JSON export/import.
- Official source links and simple keyword filtering.

## Privacy

The source contains no real student audit, student ID, GPA, name, transcript, academic profile, or user-specific graduation targets. The default profile is empty. The optional sample is fictional. Course records are stored in browser localStorage and are not sent to a backend. An exported plan may contain personal information; keep it private. Reset clears the current workspace in that browser. Visiting official source links or the GitHub link contacts those external services.

## Rule snapshot and limits

Rules are based on the [MSCS degree requirements](https://www.cc.gatech.edu/degree-programs/master-science-computer-science) and [June 2026 Machine Learning program-of-study worksheet](https://www.cc.gatech.edu/sites/default/files/documents/2026/ML%20POS%20updated%20June%202026.pdf). These are fixed snapshots, not continuously synchronized policy feeds.

The coursework degree requires 30 credits: 6 core, 9 ML electives, and 15 free electives, plus the program's graduate-level and grade constraints. The app includes selected worksheet courses, not the full list. Unlisted courses are treated as **provisional free electives**, not approved credits. The default course credit count is 3 and is editable.

Current checks do not validate GPA, prerequisites, schedule conflicts, repeats/equivalencies, residency, offering dates, an individual student's applicable catalog, or approval for shared BS/MS or transferred credit. It does not audit BS threads. The project and thesis MS options are not supported. Future semester availability and graduate exchange routes must be checked separately using [OSCAR](https://oscar.gatech.edu/) and [OIE](https://ea.oie.gatech.edu/exchange-credit-transfer-instructions).

## Architecture

Buildless HTML/CSS/JavaScript. `dist/model.js` holds rules and import validation; `dist/app.js` implements the UI and browser persistence; `tests/model.test.js` tests credit allocation and import boundaries. No API key, server database or LLM is used in this release.

## Roadmap

1. Parse audit PDFs locally or through an explicitly consented backend, preserving source provenance and user confirmation.
2. Ingest versioned requirements and published course offerings into structured tables, with freshness dates.
3. Collect syllabi, course descriptions and graduate abroad policies; chunk and embed them into PostgreSQL/pgvector.
4. Retrieve evidence filtered by program, catalog year and course. An LLM explains computed plans using citations and abstains where evidence is missing.
5. Evaluate retrieval recall, citation support, credit matching and missing-evidence behavior. Track latency, tokens and estimated request cost.
6. Expose evidence search and requirement gaps through an MCP server; deploy the API on GCP.

## Contributing

Use synthetic records in issues, fixtures and screenshots. Never commit a real audit or exported personal plan. Propose rule updates with an official source and a focused validation case.

Independent project, not affiliated with or endorsed by Georgia Tech.
