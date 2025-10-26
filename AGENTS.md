# Repository Guidelines

## Project Structure & Module Organization
- `index.html` delivers the landing page and navigation styling used across the project.
- Individual quizzes live in `*-test.html`, each bundling HTML, CSS, and the JavaScript question bank for a single poem.
- Shared data sources belong in `data/`; keep JSON exports synchronized with the matching `questions` array embedded in the quiz files.
- Leave exploratory notes or large-language-model prompts in the existing `CLAUDE.md` file so production pages stay clean.

## Build, Test, and Development Commands
- `python3 -m http.server 8000` from the repo root serves the static site locally; browse to `http://localhost:8000/index.html`.
- `python3 -m http.server 8000 data` is useful for quickly verifying raw JSON payloads during question-bank edits.
- `npx serve@latest .` offers a live-reload-like loop if you prefer Node tooling; restart when you touch HTML or CSS.

## Coding Style & Naming Conventions
- Keep four-space indentation throughout HTML, CSS, and JavaScript; match the existing brace placement and spacing.
- Use descriptive IDs/classes (e.g., `progressFill`, `questionContainer`) and stick to camelCase for JavaScript variables.
- Extend shared gradients, typography, and card components instead of introducing divergent ad-hoc styles.
- When adding questions, follow the `{ prompt, options, correct, explanation? }` shape already present in the arrays.

## Testing Guidelines
- After edits, load the affected page in a browser, complete at least one full quiz, and watch the console for errors.
- Verify selectable question counts (10/50/100) update progress, scoring, and result summaries accurately.
- Cross-check each answer and explanation against its source text; aim for full coverage of newly added questions.
- Document manual verification steps in your PR for future reproducibility.

## Commit & Pull Request Guidelines
- Follow the existing imperative, sentence-case commit style (e.g., `Add question count selection feature to multiple tests`).
- One functional change per commit helps reviewers trace quiz logic or content adjustments.
- Pull requests should include: purpose summary, impacted files, manual test notes, and screenshots or GIFs of UI changes.
- Link related issues or discussion threads, and flag any outstanding content reviews or translation checks.

## Content Authoring Tips
- Source text should come from authoritative editions; double-check tone marks and punctuation before publishing.
- For large updates, add TODOs in `CLAUDE.md` and stage partial drafts there until they are classroom-ready.
