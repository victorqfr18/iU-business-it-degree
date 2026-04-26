# DLBCSDSJCL01 — Data Structures and Java Class Library
| Data Structures and Java Class Library (DLBCSDSJCL01) | 🔄 Attempt 3 in prep | [DLBCSDSJCL01_Java-Class-Library](./DLBCSDSJCL01_Java-Class-Library) |
**Module:** Data Structures and Java Class Library  
**Program:** B.Sc. Business IT — IU International University of Applied Sciences  
**Status:** In progress — two failed attempts, preparing for attempt 3  
**Exam format:** 15 multiple choice + 5 written questions, 50% to pass  

---

## What this module covers

Six units spanning Java's built-in tools for working with objects, organizing data, and handling files:

- **Unit 1** — Programming Style: Javadoc comments, code annotations (`@Override`, `@Deprecated`), naming conventions
- **Unit 2** — Working with Objects: `toString()`, `==` vs `equals()`, `hashCode()`, `compareTo()`, `clone()`
- **Unit 3** — External Packages & Libraries: `import` keyword, classpath, Java Class Library structure
- **Unit 4** — Data Structures: arrays, Collections framework (List, Set, Map), Stack, Queue, Iterator
- **Unit 5** — Strings & Calendar: String methods, `StringBuffer`, `split()`, `Date`, `GregorianCalendar`
- **Unit 6** — File System & Data Streams: `File` class, `Reader`/`Writer`, `InputStream`/`OutputStream`

---

## Attempt 1 — August 2025

**Result:** Failed  

**What went wrong:** Studied by reading the course book only. No drilling, no practice questions, no code tracing. Read through the material, assumed understanding, and sat the exam without testing myself on anything. The result was predictable — recognition without recall.

**Root cause:** Passive study. Reading without doing.

---

## Attempt 2 — April 2026

**Result:** Failed  

**What went wrong:** Changed approach significantly — used puzzle-first learning (predict code output before explanation) and drilled with MC-style questions across all 6 units. Scored an estimated 75–85% on multiple choice sections across several practice runs. However, the written section required writing code from scratch, and I couldn't produce it.

Specific failures on the exam:

- Wrote `TreeSet<int>` instead of `TreeSet<Integer>` — collections require wrapper classes, not primitives
- Wrote `LinkedList<double>` instead of `LinkedList<Double>` — same error
- Missed the `String.replace()` immutability trap — `replace()` returns a new string but I forgot to assign it back, even after drilling this concept three separate times
- Could not name the five requirements of `equals()` (reflexive, symmetric, transitive, consistent, null-safe)
- Could not create a `Date` object using `GregorianCalendar` with correct zero-indexed month syntax
- Did not know `String.valueOf()` for converting primitives to strings
- Could not write `equals()`, `clone()`, or `compareTo()` method implementations from scratch

**Root cause:** Preparation was MC-only. Every drill was recognition-based — I could read code and pick the right answer, but I never practiced writing code from a blank page. The exam's written section exposed this gap completely. Understanding a concept and being able to produce it under pressure are two different skills, and I only trained the first one.

---

## What's changing for Attempt 3

### Two-phase drilling for every concept

Every topic now gets drilled twice:

1. **Phase 1 — Recognition:** Code puzzles and MC questions (what does this print? which answer is correct?)
2. **Phase 2 — Production:** Write the code from scratch on paper with no reference material. If I can't produce it from a blank page, it's not learned.

### Specific weak spots to target

| Priority | Topic | Why it failed |
|----------|-------|---------------|
| Critical | Wrapper classes in code (`int`→`Integer`, `double`→`Double`) | Understood concept, couldn't produce correct syntax |
| Critical | String immutability under exam pressure | Knew the rule, failed to apply it when it mattered |
| Critical | Five `equals()` requirements by name | Taught once as a list, never drilled individually |
| Critical | `GregorianCalendar` creation (zero-indexed months) | Never wrote this code from scratch |
| Critical | `String.valueOf()` for primitive-to-String conversion | Never drilled |
| Critical | Date object creation and formatting with `SimpleDateFormat` | Created a String instead of a Date object on the exam |
| High | Writing `equals()`, `clone()`, `compareTo()` implementations | Can explain the pattern, can't write the code cold |
| High | Collection declarations with proper generics | Can read `HashMap<Integer, String>`, can't write it unprompted |
| Moderate | `ArrayList` vs `LinkedList` performance differences | Got it backwards once |
| Moderate | `Map.put()` with duplicate key — overwrites value, size stays same | Got size wrong under pressure |
| Moderate | Override vs Overload distinction | Learned same day as exam, may not be locked in |

### Study method that works

- **Puzzle-first format:** Show code → predict output → explain after. Walls of text kill engagement.
- **Real-world analogies:** Cinema seats for ArrayList, chain of people for LinkedList, phone contacts for Map, stack of plates for Stack.
- **Handwritten notebook:** One cheat-sheet page per unit, corrections written after every wrong answer.
- **Hard stop rule:** No skipping hard topics under time pressure, no moving forward until a concept is locked.

---

## Lessons learned

1. Reading without doing doesn't work. (Attempt 1)
2. Recognition without production doesn't work either. (Attempt 2)
3. The only thing that works is being able to produce the answer from nothing — no options to choose from, no code to trace, just a blank page and a question.
