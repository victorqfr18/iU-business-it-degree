# Flashcards

A flashcard quiz that takes its decks from my Claude university project. Single HTML file, no build step, progress saved in the browser.

Live: https://victorqfr18.github.io/iU-business-it-degree/flashcards/

## How it links to Claude

1. Paste [`CLAUDE_PROJECT.md`](CLAUDE_PROJECT.md) (the part below the line) into the Claude project's instructions.
2. Ask Claude in the project for flashcards on whatever I'm studying. It answers with a JSON deck.
3. **Import deck** → paste. Re-importing a deck with the same `id` updates its cards and keeps progress.
4. After a session, **Copy report for Claude** puts the missed cards (with my wrong answers) on the clipboard. Paste it into the project and Claude re-teaches them and sends a follow-up deck.

## Card types

| Type | What happens | Good for |
| --- | --- | --- |
| `mc` | Pick one of the choices (shuffled) | Code-output puzzles, trap options |
| `input` | Type a short answer, checked automatically | One-line declarations, keywords |
| `write` | Write from memory, reveal, grade yourself | Method implementations, lists to recall |

## Study modes

- **Study**: cards that are due plus new ones, 20 per session.
- **Drill mistakes**: the cards with the worst record.
- **Everything**: the whole deck (or one unit, using the unit filter).

A missed card comes back a few cards later in the same session until it's answered correctly. Scheduling is a simple Leitner system: right moves a card up a box (due in 1, 3, 7, 16, 35 days), wrong drops it to box 1. "Locked in" means box 5 or higher.

## Built-in decks

Decks in [`decks/`](decks) listed in `decks/index.json` load automatically on the hosted site. To make a deck permanent (and available on every device), save Claude's JSON as `decks/<id>.json` and add the file name to `decks/index.json`. Imported decks live only in the browser they were imported in.

Opened straight from disk (`file://`), the browser blocks loading `decks/`, so only imported decks show. Use the hosted site or `python3 -m http.server` in this folder.

## Keys

| Key | Action |
| --- | --- |
| 1–4 | Pick a multiple-choice answer |
| Enter | Check a typed answer / continue |
| Ctrl+Enter (⌘+Enter) | Reveal a written answer |
| 1 / 2 | Missed it / got it, after revealing |
