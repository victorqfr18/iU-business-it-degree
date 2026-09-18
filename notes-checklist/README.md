# Notes

A single-file checklist notebook styled after the iPhone Notes app. No build step, no dependencies, no account. Open `index.html` in any browser or host it on GitHub Pages.

## What it does

- Notes list with search, grouped by Today / Yesterday / Previous 7 Days, sorted by last edit.
- Note editor with Title, Heading, Body, bulleted lists and checklists, plus bold / italic / underline / strikethrough.
- Everything saves to the browser automatically (localStorage). Nothing leaves your device.
- Undo and redo inside a note, and Undo after deleting a note or clearing checked items.
- Progress readout ("3 of 8 done") on the note and in the list.
- Light and dark mode follow the system setting.
- Works on phones: the list and the note slide like the iPhone app.

## Shortcuts

| Action | Mac | Windows / Linux |
| --- | --- | --- |
| Checklist | ⌘ ⇧ L | Ctrl Shift L |
| Bulleted list | ⌘ ⇧ 7 | Ctrl Shift 7 |
| Title / Heading / Body | ⌘ ⇧ T / H / B | Ctrl Shift T / H / B |
| Check or uncheck the current item | ⌘ ⇧ U | Ctrl Shift U |
| Bold / Italic / Underline | ⌘ B / I / U | Ctrl B / I / U |
| Undo / Redo | ⌘ Z / ⌘ ⇧ Z | Ctrl Z / Ctrl Y |
| New note | ⌘ ⌥ N | Ctrl Alt N |
| Search | ⌘ F | Ctrl F |

The first line of a note is always its title. Pressing the checklist button while on the title starts a checklist right below it.

While typing, at the start of any other line: `[] ` starts a checklist item, `[x] ` a checked one, `- ` a bullet and `## ` a heading. Enter on an empty list item ends the list. Backspace at the start of a list item turns it back into text. To turn existing lines into a checklist, select them (or just put the cursor on one) and press the checklist button.

Pasted text keeps its structure: lines starting with `[ ]`, `[x]`, `-` or `•` become list items.
