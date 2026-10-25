# Copilot instructions

## Project shape

- This is a dependency-free static web app. The entire application is in `index.html`, including markup, CSS, question data, and browser-side JavaScript.
- There is no build pipeline or server requirement; open `index.html` directly in a browser to run it.

## Architecture and behavior

- The `questions` array in the inline script is the source of truth for quiz content and correct answers.
- Quiz state is held in `currentQuestion`, `score`, and `answered`. `renderQuestion()` creates the answer buttons and resets question feedback; `chooseAnswer()` locks the choices and updates score and feedback; the Next button advances the question and progress; `showResults()` renders the score-based result; `restart()` resets the state and returns to question one. Keep these transitions and their displayed state in sync.
- The page has two views inside the card: `#quiz` and `#result`. The card's `aria-labelledby` changes with the active view, so preserve that relationship when changing how the result screen is rendered.

## UI and accessibility conventions

- Keep styles in the inline `<style>` block and use the existing CSS custom properties for colors. When adding or changing a theme color, update both `:root` and `@media (prefers-color-scheme: dark)`.
- The interface uses semantic headings and native buttons. Preserve visible `:focus-visible` styles, focus movement to the next question or result, the progress bar's ARIA values, and live announcements for feedback and results.
- Animations have a `prefers-reduced-motion` override; account for it when adding motion.
- Create answer labels as text, not HTML. The current renderer uses `textContent` for the answer label.

## Build, test, and lint

- No package manifest, build scripts, automated test runner, or linter is present, so there are no repository-defined build, single-test, or lint commands.
- For a browser smoke check, open `index.html` directly and verify an answer can be selected, score and progress update, the quiz reaches its results screen, and Play again resets it.
