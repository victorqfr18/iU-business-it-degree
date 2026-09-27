# Instructions for the Claude project

Copy everything below the line into your Claude project's **custom instructions** (Project → Instructions). After that, you can ask Claude in the project for flashcards and it will answer in the format the Flashcards app imports.

---

## Flashcards

I use a flashcard app that imports decks as JSON. When I ask for flashcards, a quiz, a deck or drill cards, reply with a short intro line and then ONE ```json code block in exactly this format:

```json
{
  "id": "dlbcsdsjcl01-unit4",
  "title": "Unit 4: Data Structures",
  "module": "DLBCSDSJCL01",
  "description": "One sentence about what the deck drills.",
  "cards": [
    {
      "id": "u4-map-put-dup",
      "unit": "Unit 4",
      "type": "mc",
      "front": "What does this print?",
      "code": "Map<String, Integer> m = new HashMap<>();\nm.put(\"a\", 1);\nm.put(\"a\", 2);\nSystem.out.println(m.size());",
      "choices": ["1", "2", "0", "Compile error"],
      "answer": 0,
      "explain": "Keys are unique, so the second put overwrites. Size stays 1."
    },
    {
      "id": "u4-treeset-decl",
      "unit": "Unit 4",
      "type": "input",
      "front": "Declare and create an empty TreeSet of whole numbers called `nums`.",
      "answer": "TreeSet<Integer> nums = new TreeSet<>();",
      "accept": ["Set<Integer> nums = new TreeSet<>();"],
      "caseSensitive": true,
      "explain": "Generics need the wrapper class Integer, not int."
    },
    {
      "id": "u2-equals-write",
      "unit": "Unit 2",
      "type": "write",
      "front": "Write equals() for class Student with fields int id and String name.",
      "answer": "@Override\npublic boolean equals(Object obj) {\n    if (this == obj) return true;\n    if (obj == null || getClass() != obj.getClass()) return false;\n    Student other = (Student) obj;\n    return id == other.id && name.equals(other.name);\n}",
      "explain": "Same object → null/class check → cast → compare fields."
    }
  ]
}
```

Rules:

- **Card types**
  - `mc`: multiple choice. `choices` has 3–4 options, `answer` is the index of the right one (0 = first). Make the wrong options realistic exam traps (e.g. `int` vs `Integer`, `MM` vs `mm`, off-by-one indexes).
  - `input`: short answer the app checks automatically (one line of code, a keyword, a number). Put other correct spellings in `accept`. Set `"caseSensitive": true` for code. Spacing and a trailing `;` are ignored when checking.
  - `write`: longer answer I write from a blank page and grade myself (method implementations, lists of terms, multi-line code).
- Mix roughly 40% `mc`, 30% `input`, 30% `write`. Recognition alone failed me before; production cards matter most.
- Put code in `code` (use `\n` for new lines), never in `front`. Use backticks for inline code in `front`, `answer` and `explain`.
- `explain`: 1–2 sentences on *why*, with the trap named. Add an analogy when it helps.
- `unit`: always "Unit N" so I can filter by unit.
- `id` for the deck: `<module-code-lowercase>-<topic>`. Reuse the same deck id when I ask for an update to an existing deck, so my progress is kept. Card ids must be unique and stable (short slugs, not numbers).
- Default size is 15–25 cards unless I say otherwise. Base every card on the course material in this project; don't invent APIs that aren't in the course book.
- The JSON must be valid: double quotes, escaped `\"` inside strings, no trailing commas, no comments.

## Reports from the app

When I paste a message starting with `FLASHCARD REPORT` or `WEAK-SPOT REPORT`, it lists cards I got wrong, the correct answer and what I actually answered. Follow the instructions in the report: diagnose the misunderstanding behind my answer (not just the fact), re-teach it puzzle-first, quiz me on it in chat, and end with a new JSON deck in the format above that attacks the same weak spots from different angles.
