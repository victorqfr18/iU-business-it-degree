# Flashcards

A flashcard quiz for my IU modules. One HTML file, no build step, two ways to run it:

- **On claude.ai, with Claude built in:** https://claude.ai/artifact/7oydLcwvP2euRu1nZPCTLU (private to my account). The page asks Claude directly on my Claude plan, and decks, progress, chats and course notes are saved to my claude.ai account, so they follow me between devices.
- **On GitHub Pages:** https://victorqfr18.github.io/iU-business-it-degree/flashcards/. Same app, but Claude is reached by copy and paste through my Claude project, and everything is saved in the browser.

The page switches automatically: when it can reach Claude (`window.claude.use("sample")`) the Claude features appear and the copy/paste buttons hide.

## Claude built in (claude.ai version)

- **Course notes** per module (Edit → paste text, or add .pdf/.txt/.md files). Claude bases every card and answer on them; long notes are searched for the parts that match the question.
- **Make cards**: type a topic, press Make cards, and a new deck of about 15 cards lands in the module.
- **Chat**: the text box talks to Claude about the module. It knows my weak spots. Asking for a quiz returns a deck with an "Add" button.
- **In a quiz**: *Ask Claude why* after a miss explains the misunderstanding behind my answer. *Grade with Claude* marks a written answer like an exam marker before I confirm.
- **After a session**: *Explain my mistakes* and *Make a follow-up deck*. On a deck: *New cards for my weak spots*.

To update the claude.ai page after changing `index.html`, Claude republishes it (the published copy is `index.html` without the `<html>/<head>/<body>` wrapper, plus `decks/` and `CLAUDE_PROJECT.md`).

## Modules

The layout follows claude.ai projects: a sidebar with a folder for each module, and a module page with a Claude-style text box, the module's decks, and a side panel with its Claude project link. **New module** adds a folder, **Edit** renames it, changes its code or deletes it. A module shows the decks whose `module` matches its code, and a badge on the folder counts the cards due. On a phone the sidebar opens from the button at the top left. Everything is saved in the browser.

## How it links to Claude

A website can't read claude.ai chats, so the link is one tap each way:

1. Paste [`CLAUDE_PROJECT.md`](CLAUDE_PROJECT.md) (the part below the line) into the Claude project's instructions.
2. On the module page, press **Edit** and paste the project's address (`https://claude.ai/project/…`).
3. Type what I'm studying now and press **Get cards** (or Enter in the text box). It copies a prompt (module, topic, deck id, the decks I already have) and opens the project. Paste it into a new chat and send.
4. Copy Claude's reply, come back and press **Paste deck**. The deck lands in the folder for its `module` (a new folder is made if none exists). Re-importing a deck with the same `id` updates its cards and keeps progress.
5. After a session, **Send report to Claude** copies the missed cards (with my wrong answers) and opens the project again, so Claude re-teaches them and sends a follow-up deck.

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
