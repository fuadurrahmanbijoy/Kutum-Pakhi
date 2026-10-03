# build-chapter

**Role.** Writes one chapter package for the course described in this file. Input: a chapter number in the prompt. Output: `chNN-package.zip` and nothing else.

**Start.** Attach this file and say: *Start with build-chapter, chapter 7.* Any form of the number works (7, ch7, ch07, chapter 7, chap-7). The appendix is `A1`.

**Run (agent: follow exactly, add nothing).**

1. Read the code from the prompt. Normalise it to the folder code `ch07` (appendix: `a1`) and the entry key `CH07` (appendix: `A1`). If no number is given, ask for it and stop.
2. Use only three parts of this file: `## GLOBAL`, `## METHOD`, and the single entry `=== CH07 ===`. Ignore every other entry. If this file is already in your context, use those parts from there. If it is only on disk, print just those parts:
   - `awk '/^## GLOBAL/{f=1} /^<<<CHECK>>>$/{f=0} f' build-chapter.md` for GLOBAL and METHOD
   - `awk -v c=CH07 '/^=== /{p=($2==c)} p' build-chapter.md` for the entry
3. Begin your reply with one line: the code and the entry's title. Then write the files into a folder named `ch07/`, in this order, in parts of about 3,000 words (create, then append; never reprint):
   - `ch07-chapter.md`
   - `ch07-answers.md`
   - `ch07-glossary.md`
   - `ch07-plate.svg` (the opening engraving, from the entry's `plate:`; the appendix has none)
   - `ch07-fig01.svg`, `ch07-fig02.svg`, … exactly as many as the entry's `figures:` says
4. Zip the files flat (no folder inside) as `ch07-package.zip` and deliver it at once (in a chat environment, save it to the outputs folder and present it).
5. Then validate. Extract the checker and run it: `awk '/^<<<CHECK>>>$/{f=1;next} /^<<<END>>>$/{f=0} f' build-chapter.md > check.py` then `python3 check.py ch07 build-chapter.md`. It prints `ok` or failures. Fix each failure with a small `str_replace` patch in the same file, rebuild the zip under the same name, and deliver it again. Never rewrite a file to fix a few lines. Do not rerun the checker unless a patch touched more than a few lines.
6. End with one line: `ch07 done.` If any fact needs the reader's check, add one line `Verify:` with the items. Nothing else.

**Token rules.** No preamble, no restating this file, no explanation of choices, no self-review prose, no reading a file back after writing it, no previews. Check only with the script. Output tagged text and SVG only; never HTML, CSS or page layout.

**Facts.** Make one targeted web search on this chapter's historical case (the entry's `history:`), if search is available. Use only settled, well-known facts elsewhere. Cut anything you cannot support, or list it under `Verify:`.

**The entry is the single source.** Use the entry's figures, terms, titles and cross-references exactly as written. You know nothing about other chapters except what the entry and GLOBAL say. Never mention objectives, topics, exams, marks, years of papers, or past papers.

## GLOBAL
course: MGT 102
book: MGT 102
spelling: British · dates: day, month, year (12 March 2026) · country: mixed, no single country; the running case's home is Bangladesh, examples and history draw on several countries, and the place is named whenever law or standards differ · currency and numbers: taka for the running case, written Tk 158,000 (international digit grouping); a historical case keeps its own currency
running case: Meghna and Sons — illustrative. Base facts (FIXED): a family-run bookshop in Dhanmondi, Dhaka, founded 3 February 1996 by Harun Meghna (owner); at 1 January 2026, 14 people (the owner and 13 employees); sales 2025 Tk 18,600,000; profit 2025 Tk 1,240,000; rent Tk 200,000 per month; shown as a documented case file, with no dialogue and no invented feelings
chosen words (one term, one word):
- use organisation — also firm, enterprise, company, business
- use manager — also executive, administrator, supervisor (for the role in general)
- use employee — also worker, staff member
- use subordinate — also junior, report
- use objective — also goal, aim, target (in case figures a sales figure is written as a sales objective)
- use standard — also benchmark, yardstick
- use span of management — also span of control
- use controlling — for the function; also called control as a general word, monitoring only for regular watching
- use leader — also head, chief (when the sense is influence)
- use environment — also surroundings, setting
size plan: 12 chapters and A1, ~57400 words, ~243 pages
chapters:
1. What Management Is
2. Managers: Levels, Skills and Standing
3. How Management Thought Developed
4. Environment, Ethics and Social Responsibility
5. Planning
6. Objectives and Management by Objectives
7. Decision Making
8. Organising: Process and Structure
9. Span, Departments, Authority and Coordination
10. People, Motivation and Creativity
11. Leadership
12. Controlling
A1. Maths You Will Use

## METHOD

### 1. The reader

- A first-year student with **no prior knowledge** of the subject. Every subject term is new.
- Comfortable with arithmetic and basic algebra; vocabulary and unfamiliar ideas are the barrier.
- English is a second language: fluent in everyday speech. Technical words need a **simple definition in English, not a translation**.
- Intelligent and motivated: a beginner in the subject, not in thinking.

**Rule:** never assume the word, never assume the idea, never assume the reader is slow.

### 2. Voice and tone

One character: serious, clear, never condescending. The register changes with the job.

| Register | Use it when | How it sounds |
| --- | --- | --- |
| **Storyteller** | Opening a new, complex idea | A puzzle or a moment of tension; the reader wants the answer |
| **Plain authority** | Definitions, rules, principles | Short, exact sentences; no ornament |
| **Patient tutor** | Worked examples and procedures | "We" and "you"; each step announced and explained |
| **Measured professor** | Framing, history, judgement | Dignified, slightly formal, suited to a Victorian-style book |

Tone: encouraging without being patronising. Treat confusion as normal and explainable. Be honest about difficulty, sparingly (*"Many students find this step confusing, because…"*) and then remove the confusion. Never imply the reader should already know something. Give any unfamiliar name from history (person, place, company) one line of context: who, when, where. No jokes at the reader's expense; wit only when it helps an idea stick. Clear is not casual.

### 3. Language

- **Sentences.** New or complex material: 12 to 18 words on average, one idea per sentence when defining. Elsewhere: 18 to 22. Vary the length; a short sentence after a long one lands well. Keep subject and verb close. No stacks of nouns. If "it" could mean two things, repeat the noun.
- **Active voice** and everyday words. Choose the plain word over the grand one when both are correct.
- **Never use:** idioms or figures of speech that do not translate; slang; phrasal verbs where one clear verb exists (*carry out* becomes *perform*, *set up* becomes *establish*, used consistently); hedging stacks (*it could perhaps be argued that…*); and words that dismiss difficulty: *simply, just, obviously, clearly, of course, as everyone knows*.
- **One term, one meaning, one word.** Where a concept has several names, mention the equivalents once, in one sentence, then use only the chosen word from GLOBAL. Never vary a term for style.
- Never hurry. If a step matters, give it room.
- Never use `^` except for footnotes. Write powers as ², ³ or in words ("to the power of 4").

### 4. Defining terms

A new term appears in **bold** (plain bold) at first use, and its definition follows at once:

1. The term in bold.
2. *means* or *is*, plus a plain definition of about 20 words or fewer, in words simpler than the term.
3. A tiny example in the next sentence.
4. A side note repeating the definition in one line: `@ Term | definition`.
5. A glossary entry (fuller definition) in the glossary file.

Rules: never define with a technical term the reader has not met (define that one first); never define in a circle; no translations. After first use the term is ordinary type. Bold is only for key terms at first appearance, never for emphasis. Italics are for emphasis, foreign words and titles of works.

**This chapter defines exactly the terms in its entry's `defines:`, no more and no fewer.** Terms in `assumes:` may be used but are never defined and never bold. If a term from a later chapter is needed early, give a one-line plain-word preview, not bold, and point to where it is taught (chapter, section number and title).

**Words with two meanings** (everyday words with a special subject meaning, such as *account, capital, stock, interest, margin, cost, value, current, goods, balance*, and others the entry lists under `words-in-use:`): add a "Word in use" note, at most three per chapter, only where confusion is likely:

```
@ Account | Word in use. In daily life, a record of money in a bank. In accounting, a named record of one kind of item, such as Cash or Sales.
```

### 5. Which approach for which topic

| Kind of topic | Open with | Then |
| --- | --- | --- |
| New, complex idea (never met) | A puzzle or question, in storyteller mode | Build the idea in layers; end with the plain rule |
| Existing framework or phenomenon | A puzzle, then a concrete example | Draw out the general principle; state the rule; note exceptions |
| Technique or procedure | A concrete example | Worked example in tutor mode; formula afterwards |
| Defining theory with a known origin | A short historical hook | Explain the idea; connect it to a modern case |

When in doubt, start with a question the reader can almost answer.

### 6. The layered spine

Every concept follows this order: **idea** (plain words, why it matters, a puzzle where suitable) → **example** (from the running case or history) → **rule** (definition, principle or formula, stated precisely) → **exceptions** (limits, where it fails, common confusions). Weave in, briefly: **by questions** (What is it? Why does it exist? How does it work? Where does it fail?) to check no layer is missing; **by viewpoint** (owner, manager, employee, customer), a sentence or short paragraph; **by stages** (simple first, detail after the simple version is secure; mark advanced material clearly so a beginner can defer it).

### 7. Length

| Tier | Covers | Length |
| --- | --- | --- |
| **Minor** | Vocabulary, small distinctions | 3 to 8 lines (never fewer than three visible lines), plus a side note |
| **Standard** | Most ideas | 150–300 words |
| **Core** | The idea the section exists to teach | 400–700 words, with an example and exceptions |
| **Landmark** | A defining idea of the discipline | 800–1,500 words, with history, worked example, subsections, moderate citation |

Length follows importance, never frequency. It must never feel hurried or padded. A concept that is new to the reader moves up one tier. **Paragraphs:** one idea each, 4 to 10 lines, and each must be summarisable in one line (the side column carries that summary). **Chapter:** the length in the entry's `words:`; the opening puzzle is half to one page.

### 8. Pace: two speeds

**Standard pace.** Introduce new ideas in small groups (two or three per section). End every section with a recap of two or three lines, written as a paragraph that begins *Before moving on.* in italics. Follow the spine.

**Slow pace.** Use it when a concept is both new and abstract, has more than three moving parts, or depends on an earlier idea that may not have stuck (examples: opportunity cost, double-entry, accruals, marginal analysis, elasticity, the time value of money). In slow pace:

1. One idea at a time; finish one before starting the next.
2. An everyday bridge first (a household budget, a market stall, a part-time job), then the subject version.
3. Two forms of the same idea: words, then a simple diagram or a tiny numerical example.
4. The smallest possible numbers in the first example.
5. A recap after each idea, not only at the end of the section.
6. A closing line: *You should now be able to say…* (one sentence the reader can test against).
7. A side flag: `@! Go slowly here.`

Where the entry says `pace: slow`, the whole chapter leans slow. After slow passages place one or two `:pause` questions.

### 9. Ordering: nothing before its time

- Never use a term before it is introduced. If one must appear early, give a one-line preview and point to where it is taught.
- Open with a "You will need" note built from the entry's `need:` (chapter and section names; no page numbers).
- Start from the reader's own experience (spending, saving, buying, selling) and move to the subject: the everyday bridge first, the subject case confirms it.
- Build each idea on what came before. Early figures are small and round; they grow realistic as confidence grows.

### 10. Examples: two tracks

**Track A: the running case.** Use only the facts in the entry's `case:`, exactly as given; never invent or change a figure. Present it as a documented case file, not a story: dates, figures, decisions, records; no dialogue, no feelings, no narrative colour. Every `:case` paragraph begins *Case file, illustrative.* so no reader mistakes it for a real organisation.

**Track B: a real historical case** (the entry's `history:`). Short, factual, dated, attributed. Never invent history. If a date, figure or quote cannot be verified, leave it out. Prefer settled facts; date any current figures. State which country's rules apply when law, tax or standards differ by place.

### 11. Numbers and calculations (calculation and mixed chapters)

Students must be able to do this by hand in an exam. Never skip a step. Every formula or calculation gets a worked example in this order: **Given** (the data), **Find** (what is asked), **Formula** (in words first, then in symbols, saying what each symbol stands for), **Steps** (every line of arithmetic, with units), **Answer** (in a sentence), **Check** (a quick test that it is sensible).

Progression: first example small and clean, so the method is the only thing to learn; second slightly messier and realistic; then a note on **common slips** (wrong sign, forgotten units, mixed-up periods); practice problems close the chapter. Explain where a formula comes from in a line or two when it helps; full derivations only for landmark formulas. The first time a chart appears, say how to read it: what the axes show and what a point means.

### 12. Descriptive chapters

Replace "worked example" with a **worked case**: *Situation, Question, Reasoning, Conclusion, Check.* It applies an idea to a situation; it is not a model exam answer. Replace the change-the-numbers ladder with a change-the-**situation** ladder: a familiar case, a reshaped case, a new setting, a case that combines earlier ideas. Show distinctions in a short comparison table, introduced in words first; the text explains how to read a row. The book never contains model exam answers or advice on writing them; it builds understanding complete enough that a reader can answer.

### 13. Repetition without boredom

Each key idea returns in different forms: in the text; in its side note; in the *Before moving on* recap; in the chapter summary and review questions; and in later chapters as a short recall note in the side column, written from the entry's `assumes:` and `refs:` (*Recall: opportunity cost, Chapter 3, section 3.2.*). Place one or two `:pause` questions after slow passages.

### 14. Referencing and cross-references

- **Light by default:** name the thinker and year in the text (*Fayol, 1916*). **Moderate for defining topics** (entry says `sources: yes`): cite the founder or landmark work by name, with a short note on why it mattered, in the closing *Sources* section.
- Clarifications and side points go in footnotes. Paraphrase and credit; never quote long passages.
- List a few further-reading items as `:read` lines at the end of the chapter (author, title, year); the book collects them into one list.
- **Cross-references** use chapter number, chapter title, section number and section title, in the side column or a footnote, taken from the entry's `refs:`. Never page numbers.

### 15. Chapter shape

1. Opener tags: `:chapter`, `:mood`, `:desc`, and `:plate` (chapters only).
2. The opening puzzle (half to one page), with no heading; it makes the chapter necessary.
3. The sections in the entry (`##` headings), each following the spine and ending with a recap.
4. The worked case or worked example, as its own `##` section whose heading contains the word *Worked*.
5. The closing pack, as `##` headings in this exact order and wording: **Summary** (a few lines); **Think It Through** (a short problem or case, as `:q` items); **Where People Go Wrong** (common misunderstandings, stated and corrected); **In History** (a true account, from the entry's `history:`); **Sources** (only if the entry says `sources: yes`); **Review Questions** (`:q` items, from the entry's `practice:`).
6. `:read` lines, if any.

Opening puzzle through closing pack must stay within the entry's `words:` (plus or minus 10%; count with `wc -w`, never by feel). Use a definition box (`:box`) once or twice per chapter, no more. Use `* * *` between major parts.

**Appendix A1** is a reference, not a lesson: no opener, no closing pack, no questions. Start with `:chapter A1 | Maths You Will Use`, then short `##` topics, each a plain definition and one tiny worked example; its answers and glossary files exist but may hold only the `:answers` / `:glossary` line.

### 16. Markup (tagged text)

One chapter is one `.md` file. A blank line ends a paragraph. A line that ends without a blank line continues the paragraph.

```
:chapter VII | The Partnership         chapter number in Roman numerals, then title (first line)
:mood <one short phrase>               italic line under the title (a question or an image)
:desc <3 to 4 lines of description>    opener page description (one line of text)
## Heading                             section heading
### Heading                            subsection heading
> one-line summary                     side note summarising the NEXT paragraph
@ Term | one-line definition           key-term side note for the next paragraph
@! Go slowly here.                     slow-pace flag in the side column
**term**                               bold, first appearance of a key term only
*word*                                 italic: emphasis, foreign words, titles
^1 in text; ^1: note on its own line   footnote reference and its text (numbered in chapter order)
* * *                                  ornament between major parts
:case Case file, illustrative. …       a case-file paragraph (still needs a > summary)
:table Caption                         then rows: | Head | Head | then | cell | cell |
:fig Caption | ch07-fig01.svg          figure; the book numbers it (Fig. 7.1); never type the number
:box LABEL                             then one paragraph on the next line (for example IN SHORT)
:q 7.1 | question text                  review question (Think It Through: 7.t1, 7.t2…)
:pause 7.p1 | question text            Pause and check question inside a section
:read Author, Title, Year              a further-reading item
:plate ch07-plate.svg | caption         the chapter's opening engraving (required in chapters; no figure number)
:todo <note>                           reminder to yourself; the checker rejects any left in the file
```

**Placement.** Side-note lines (`>`, `@`, `@!`) go directly above the paragraph they belong to, in the order they should appear; a blank line between them and the paragraph is fine. Every paragraph, including every `:case` paragraph, gets a `>` summary. Add a key-term note wherever a term is defined. Introduce every table in words first. Keep every table and figure under about half a page. Tables have horizontal rules only; the book sets them.

**Sample (the voice in eight lines):**

```
## The Idea of Partnership

> Two people, each lacking something, decide to join forces.

Imagine that two friends, one skilled at choosing books and the other at selling them, decide to open a small bookshop together. Neither can afford the stock alone, and neither can run the shop alone. Before a single crate of books is ordered, one question stands between them and their business: who owns what, and who answers for what?

@ Partnership | Two or more people running a business together and sharing its profits.

The law gives the name **partnership** to such an arrangement. A partnership is a business owned by two or more people who have agreed to run it together and to share its profits.^1
```

### 17. Art: the opening plate and the figures (SVG)

**House style: Victorian engraving.** Every picture looks like a plate from a textbook of about 1850 to 1900: fine ink lines on blank ground, shade built from parallel hatching and cross-hatching, stippled dots for texture, steady outlines, period-correct people, clothes, tools and buildings. No gradients, no solid filled blocks except hatched ones, no modern icons, no photographic effects, no lettering inside a plate. Diagrams follow the same hand: neat technical engravings, ruled lines, plain-word labels.

**Opening plate (every chapter, exactly one).** `ch07-plate.svg`, drawn from the entry's `plate:` subject: a concrete scene or still life tied to the chapter's topic, composed for a landscape frame (`viewBox="0 0 400 260"`). Build it in layers: outline, then hatched shade, then a few details. Aim for 4 to 8 KB; the more shade you do with the hatch classes, the lighter the file. Name it in the opener: `:plate ch07-plate.svg | <a short caption phrase, no figure number>`. The appendix has no plate.

**Figures** (as many as the entry's `figures:` says; it may say zero): one idea each, `ch07-fig01.svg`, `ch07-fig02.svg`, …; `viewBox="0 0 400 250"` or similar; under about 4 KB; plain-word labels (no abbreviations at first use). The caption goes in the `:fig` line without a number. The first time a chart appears, say in the text how to read it.

**Strict rules (the checker rejects any breach):**
- One `<svg>` with a `viewBox` per file, made only of shapes, paths, lines, `text` and `g`. No `fill=`, `stroke=`, `style=`, hex codes, `<style>`, `<defs>`, patterns, gradients, filters, images, scripts, links or `url(...)`.
- **Colour comes only from classes.** The book gives every shape a near-black line and no fill; add a class only to depart from that. Stroke: `s-ink`, `s-red`, `s-blue`, `s-green`, `s-gold`, `s-mute`. Fill: `f-ink`, `f-red`, `f-blue`, `f-green`, `f-gold`, `f-mute`, `f-none`. Line: `dash`, `thin`, `thick`. **Engraved shade (ink only): `h-lines`, `h-dense`, `h-cross`, `h-dots`**, which fill a closed shape with hatching. Never use white or any "paper" colour; to leave an area blank, give it no fill.
- Use colour sparingly: a plate is mostly ink with at most one accent colour; a figure uses colour only to separate its parts.
- **Never let colour alone carry meaning.** Every distinction must also be carried by a text label, a dash pattern, hatching or position, so the figure reads in grey (the book also prints a black-and-white edition).

### 18. The answers and glossary files

**`ch07-answers.md`**: first line `:answers 07`. One line per question in the chapter, with the same ids:

```
:a 7.1 | <short answer: one to three sentences; for a calculation, the result and its key step>
```

Answer every `:q` and every `:pause`. Answers are short and agree with the entry's figures. They are answers to this book's own questions, never model exam answers.

**`ch07-glossary.md`**: first line `:glossary 07`. One line per term defined in this chapter (exactly the `@` terms, exactly the entry's `defines:`), in order of appearance:

```
Term | fuller definition in plain words, about 30 to 60 words, with a tiny example if it helps
```

### 19. Silent checks (while writing; report only failures)

1. No objectives, topics, exam years, marks, frequencies or question wording from any course file appear. *(This overrides everything.)*
2. Every date, name, figure and legal point is verified or cut. Case-file figures equal the entry's exactly.
3. Every term is defined before it is used; bold only at first use; no later-chapter term is bold.
4. Every paragraph has a `>` summary; every footnote reference has its text; every question has an answer; every figure and the plate exist.
5. Writing checklist for each section: opens with a question or example before the rule; every concept reaches its exceptions; each paragraph is one idea; each explanation is at least three full lines; every calculation is worked in full in the standard order; a reader with no background could follow each step without guessing; no idioms, phrasal verbs or dismissive words; one word per concept; slow pace and an everyday bridge for new abstract ideas; a recap closes each section.

The script catches most of items 3 and 4 and the structural rules. Items 1, 2 and 5 are yours.

<<<CHECK>>>
import os, re, sys
code, cat = sys.argv[1], sys.argv[2]
chap = code.startswith('ch')
rd = lambda p: open(p, encoding='utf-8').read() if os.path.isfile(p) else None
P = {k: os.path.join(code, '%s-%s.md' % (code, k)) for k in ('chapter', 'answers', 'glossary')}
T, A, G = rd(P['chapter']), rd(P['answers']), rd(P['glossary'])
bad = ['missing ' + P[k] for k, v in zip(P, (T, A, G)) if v is None]
if bad: print('\n'.join(bad)); sys.exit(1)
C = rd(cat) or ''
m = re.search(r'^=== %s ===\n(.*?)(?=^=== |\Z)' % code.upper(), C, re.S | re.M)
E = m.group(1) if m else ''
if not E: bad.append('no catalogue entry for ' + code.upper())
def fld(k):
    r = re.search(r'^%s:[ \t]*(.*)$' % k, E, re.M)
    return r.group(1).strip() if r else ''
nfig = int((re.findall(r'\d+', fld('figures')) or ['0'])[0])
plan = int((re.findall(r'\d[\d,]*', fld('words')) or ['0'])[0].replace(',', ''))
src = fld('sources').lower().startswith('y')
dm = re.search(r'^defines:[ \t]*\n((?:- .*(?:\n|\Z))+)', E, re.M)
D = {x[2:].split('|')[0].strip().lower() for x in (dm.group(1).splitlines() if dm else [])}
EXAM = re.compile(r"\b(past papers?|past questions?|learning (?:objectives?|outcomes?)|course (?:objectives?|outcomes?)|syllabus|exam(?:ination)? (?:papers?|years?|questions?)|marking scheme|marks? (?:allocated|awarded|weighting)|course file)\b", re.I)
AVOID = re.compile(r"\b(simply|just(?!-in-time)|obviously|clearly|of course|as everyone knows)\b", re.I)
for name, txt in (('chapter', T), ('answers', A), ('glossary', G)):
    for n, ln in enumerate(txt.splitlines(), 1):
        for r in EXAM.finditer(ln): bad.append('%s:%d course wording "%s"' % (name, n, r[0]))
        for r in AVOID.finditer(ln): bad.append('%s:%d avoided word "%s"' % (name, n, r[0]))
st = {'buf': [], 'sum': False, 'pend': []}
bolds, refs, defs, heads, figs, qs, terms, meta = set(), set(), set(), [], [], set(), [], set()
wiu = []
def flush():
    if not st['buf']: return
    t = ' '.join(st['buf']); st['buf'] = []
    if not st['sum']: bad.append('no > summary: ' + t[:40])
    bl = [b.lower() for b in re.findall(r'\*\*(.+?)\*\*', t)]
    for tm in st['pend']:
        if not any(tm[:5].lower() in b for b in bl): bad.append('term not bold in its paragraph: ' + tm)
    for b in bl:
        if b in bolds: bad.append('bold repeated (first use only): ' + b)
        bolds.add(b)
    refs.update(re.findall(r'\^(\d+)', t))
    st['sum'] = False; st['pend'] = []
def blk():
    flush(); st['sum'] = False; st['pend'] = []
SP = re.compile(r'(:\w|> |@!? |#{2,3} |\^\d+:|\* \* \*$)')
L = T.splitlines(); i = 0
while i < len(L):
    s = L[i].rstrip(); i += 1
    m = re.match(r':(\w+)', s)
    if m and m[1] in ('chapter', 'mood', 'desc', 'plate'): meta.add(m[1]); continue
    if m and m[1] == 'todo': flush(); bad.append('todo left: ' + s[:40]); continue
    if not s.strip(): flush(); continue
    if st['buf'] and not SP.match(s): st['buf'].append(s); continue
    flush()
    if s.startswith('### '): blk()
    elif s.startswith('## '): blk(); heads.append(s[3:].strip().lower())
    elif s.startswith('> '): st['sum'] = True
    elif s.startswith('@! '): pass
    elif s.startswith('@ '):
        if '|' not in s: bad.append('bad term note: ' + s[:40])
        else:
            tm, d = [x.strip() for x in s[2:].split('|', 1)]
            if d.lower().startswith('word in use'): wiu.append(tm)
            else: st['pend'].append(tm); terms.append((tm, d))
    elif s.strip() == '* * *': blk()
    elif re.match(r'\^\d+:', s): defs.add(re.match(r'\^(\d+):', s)[1])
    elif s.startswith(':case '): st['buf'].append(s[6:])
    elif s.startswith(':table '):
        while i < len(L) and L[i].lstrip().startswith('|'): i += 1
        blk()
    elif s.startswith(':fig '):
        figs.append(s[5:].partition('|')[2].strip()); blk()
    elif s.startswith(':box '):
        while i < len(L) and L[i].strip(): i += 1
        blk()
    elif re.match(r':(?:q|pause) ', s):
        q = re.match(r':(?:q|pause) (\S+) \|', s)
        if q: qs.add(q[1])
        else: bad.append('bad question line: ' + s[:40])
        blk()
    elif s.startswith(':read '): pass
    elif s.startswith(':'): bad.append('unknown tag: ' + s[:30])
    else: st['buf'].append(s)
flush()
for n in sorted(refs - defs): bad.append('footnote %s cited but not defined' % n)
for n in sorted(defs - refs): bad.append('footnote %s defined but never cited' % n)
if chap:
    for k in ('chapter', 'mood', 'desc'):
        if k not in meta: bad.append('missing :' + k)
    need = ['summary', 'think it through', 'where people go wrong', 'in history'] + (['sources'] if src else []) + ['review questions']
    pos = [heads.index(h) if h in heads else -1 for h in need]
    if -1 in pos or pos != sorted(pos): bad.append('closing pack headings missing or out of order: ' + ', '.join(need))
    else:
        nb = pos[0]
        if not 3 <= nb <= 7: bad.append('%d body sections before Summary (need 3 to 7, worked case included)' % nb)
        if not any('worked' in h for h in heads[:nb]): bad.append('no section heading containing "Worked"')
    if not src and 'sources' in heads: bad.append('Sources heading but entry says sources: no')
    if not qs: bad.append('no :q or :pause questions')
elif 'chapter' not in meta: bad.append('missing :chapter')
if not A.lstrip().startswith(':answers'): bad.append('answers file must start with :answers')
if not G.lstrip().startswith(':glossary'): bad.append('glossary file must start with :glossary')
aid = set(re.findall(r'^:a (\S+) \|', A, re.M))
for x in sorted(qs - aid): bad.append('no answer for ' + x)
for x in sorted(aid - qs): bad.append('answer without a question: ' + x)
tt = {t.lower() for t, _ in terms}
gt = {l.split('|')[0].strip().lower() for l in G.splitlines() if '|' in l and not l.startswith(':')}
for x in sorted(tt - gt): bad.append('term not in glossary: ' + x)
for x in sorted(gt - tt): bad.append('glossary term without a side note: ' + x)
if D:
    for x in sorted(tt - D): bad.append('term not assigned to this chapter: ' + x)
    for x in sorted(D - tt): bad.append('assigned term never defined: ' + x)
if len(wiu) > 3: bad.append('more than three Word in use notes')
for f in figs:
    if not os.path.isfile(os.path.join(code, f)): bad.append('figure file missing: ' + f)
    if not re.fullmatch(r'%s-fig\d\d\.svg' % code, f): bad.append('bad figure name: ' + f)
allf = sorted(x for x in os.listdir(code) if x.endswith('.svg'))
fs = [x for x in allf if not x.endswith('-plate.svg')]
if chap:
    if 'plate' not in meta: bad.append('missing :plate')
    if '%s-plate.svg' % code not in allf: bad.append('plate file missing: %s-plate.svg' % code)
if len(figs) != nfig or len(fs) != nfig: bad.append('figures: entry says %d, chapter uses %d, folder has %d' % (nfig, len(figs), len(fs)))
for f in allf:
    s = open(os.path.join(code, f), encoding='utf-8').read()
    if 'viewBox' not in s: bad.append(f + ': no viewBox')
    if re.search(r'#[0-9a-fA-F]{3,8}\b|\b(?:fill|stroke|style)=|<(?:image|script|style|defs|pattern|use|filter|linearGradient|radialGradient|mask|clipPath)\b|href=|url\(', s): bad.append(f + ': palette classes only (no colours, style, images, scripts, links)')
    for cl in re.findall(r'class="([^"]+)"', s):
        for tk in cl.split():
            if not re.fullmatch(r'[sf]-(?:ink|red|blue|green|gold|mute|none)|dash|thin|thick|h-(?:lines|dense|cross|dots)', tk): bad.append('%s: unknown class %s' % (f, tk))
w = len(T.split())
if plan and not 0.9 * plan <= w <= 1.1 * plan: bad.append('length: %d words against a plan of %d' % (w, plan))
print('\n'.join(bad) if bad else 'ok')
sys.exit(1 if bad else 0)
<<<END>>>

=== CH01 ===
title: What Management Is
purpose: Introduce management as the work of using an organisation's resources to reach its aims, and show how its four functions form one continuing cycle.
pace: slow — first chapter; it teaches the reader how to read the book as well as the subject
style: descriptive
words: 4800
figures: 1
- fig01: the four management functions drawn as a cycle around the resources of an organisation
plate: a bookseller behind a counter among shelves of leather-bound volumes, 1880s
sections:
1.1 | Why Organisations Need Management | new idea | 550
1.2 | Defining Management | new idea | 550
1.3 | Resources and Results | new idea | 325
1.4 | The Management Process | framework | 775
concepts:
- 1.1 | Organisations and their aims | standard | needs: none
- 1.1 | Purpose of management | standard | needs: organisations and their aims
- 1.1 | Importance of management | minor | needs: purpose of management
- 1.2 | Management defined | core | needs: organisations and their aims; purpose of management
- 1.3 | Resources a manager uses | standard | needs: management defined
- 1.3 | Results as the test of management | minor | needs: resources a manager uses
- 1.4 | The four management functions | core | needs: management defined
- 1.4 | Management as a continuing cycle | standard | needs: the four management functions
defines:
- Organisation | a group of people who work together in a planned way to reach an aim that one person could not reach alone
- Employee | a person who is paid by an organisation to do work for it
- Management | the work of using the resources of an organisation to reach its aims, through four connected functions
- Manager | a person who is responsible for the work of other people and for the results of one part of an organisation
- Resource | anything an organisation uses to do its work, such as people, money, materials, premises and information
- Management function | one main kind of managerial work; there are four, and each has its own chapter in this book
- Management process | the continuing cycle in which a manager performs the four management functions again and again
assumes: none
words-in-use: function, process
case: Case file, illustrative. Meghna and Sons, a family-run bookshop in Dhanmondi, Dhaka, founded 3 February 1996 by Harun Meghna (owner). Position at 1 January 2026: 14 people (the owner and 13 employees); shop floor 2,400 square feet; rent Tk 200,000 per month. Results for 2025: sales Tk 18,600,000; profit Tk 1,240,000. Resources at 31 December 2025: people, 14; money, cash reserve Tk 1,500,000; materials, stock held at cost Tk 6,200,000; premises, the rented shop; information, a daily sales ledger and a stock list kept on a spreadsheet. Record of the four functions for 2025: on 8 December 2024 the owner wrote the 2025 sales plan, Tk 19,000,000 (planning); on 2 January 2025 he assigned each product section to a section leader (organising); a staff meeting was held every Monday at 9:30 (leading); sales were compared with the plan at the end of each month (controlling). Outcome: sales Tk 18,600,000 against the plan of Tk 19,000,000.
history: Josiah Wedgwood's pottery works at Etruria, Staffordshire, opened 1769: planned division of work, set standards and close checking of quality under one managing owner. Search hint: Wedgwood Etruria 1769 division of labour management.
refs: Chapter 3, 'How Management Thought Developed', section 3.1 'Early Ideas and Scientific Management' — how later thinkers described the work of managers; Chapter 5, 'Planning', section 5.1 'Meaning, Nature and Purpose' — planning, the first function, in full; Chapter 12, 'Controlling', section 12.1 'Meaning, Nature and Principles' — controlling, the last function, in full
need: nothing
ladder: Rung 1: a street tea stall run by one family (people, money, stock named as resources). Rung 2: a school sports day, to show management outside business. Rung 3: a village health clinic in another country, with a different set of resources. Rung 4: a small printing workshop that combines resources, results and all four functions in one year.
practice: review: say in new words what separates a manager from an employee, name the resources of a given small organisation, match short job descriptions to the four functions, explain why a result measured in one year may mislead; think: a family bakery lists its resources and results for one year, and the reader finds where a function is missing; pause: after the definition of management and after the four-function cycle.
sources: no

=== CH02 ===
title: Managers: Levels, Skills and Standing
purpose: Show who managers are, which skills they need at each level, how to judge their work, and why management is science, art and profession in different respects.
pace: slow — foundation chapter; three new skills and three easily confused measures
style: descriptive
words: 4925
figures: 2
- fig01: three levels of managers drawn as a triangle with the skill mix at each level
- fig02: productivity, effectiveness and efficiency shown side by side as inputs, outputs and aims
plate: a foreman, a manager and a proprietor in three connected offices of a mill, 1870s
sections:
2.1 | Levels and Types of Managers | new idea | 325
2.2 | Skills Managers Need | framework | 775
2.3 | Productivity, Effectiveness and Efficiency | new idea | 550
2.4 | Science, Art or Profession | new idea | 675
concepts:
- 2.1 | Three levels of managers | standard | needs: management defined
- 2.1 | Functional and general managers | minor | needs: three levels of managers
- 2.2 | Technical, human and conceptual skills | core | needs: three levels of managers
- 2.2 | Skills in the classic and the contemporary view | standard | needs: technical, human and conceptual skills
- 2.3 | Telling productivity, effectiveness and efficiency apart | core | needs: results as the test of management
- 2.4 | Management as a science | standard | needs: none
- 2.4 | Management as an art | standard | needs: none
- 2.4 | Management as a profession | standard | needs: management as a science; management as an art
defines:
- Top manager | a manager at the highest level, who sets the direction and is responsible for the whole organisation
- Middle manager | a manager between top managers and first-line managers, who turns the direction into plans for one part of the organisation
- First-line manager | a manager at the lowest level, who directs employees who do the daily work and does not manage other managers
- Functional manager | a manager responsible for one kind of work, such as buying or accounts, across the organisation
- General manager | a manager responsible for all the kinds of work of a unit, such as a branch
- Technical skill | the ability to use the methods, tools and knowledge of a particular kind of work
- Human skill | the ability to work with other people, understand them and get good work from them
- Conceptual skill | the ability to see the organisation as a whole and to understand how its parts affect one another
- Productivity | the amount of output produced for a given amount of input, such as sales for each employee
- Effectiveness | the degree to which an organisation reaches the aims it has set
- Efficiency | the use of as few resources as possible to obtain a given result
- Profession | an occupation that requires long study, follows a code of conduct and can be entered only by meeting set standards
assumes: Organisation; Employee; Management; Manager; Resource; Management function; Management process
words-in-use: level, skill
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna. Structure at 1 January 2026 (14 people): top level, the owner; middle level, three managers (Imran Meghna, purchasing; Nasrin Akter, shop floor; Rubel Hossain, accounts); first level, four section leaders (school books, general books, stationery, orders and parcels); six shop assistants. Sales: 2024 Tk 17,100,000 with 13 people; 2025 Tk 18,600,000 with 14 people. Sales for each person: 2024 Tk 1,315,385; 2025 Tk 1,328,571. Plan for 2025: Tk 19,000,000; achieved Tk 18,600,000, which is 97.9% of the plan. Unsold stock written off: 2024 Tk 310,000 (1.8% of sales); 2025 Tk 186,000 (1.0% of sales). Skill record for 2025: Imran judged which titles would sell (technical); Nasrin arranged shift rotas that all employees accepted (human); the owner decided on 8 December 2024 how the three sections and the accounts fit one plan (conceptual).
history: Robert L. Katz, 'Skills of an Effective Administrator', Harvard Business Review, 1955: the three-skill view, drawn from his observation of managers. Search hint: Katz 1955 skills of an effective administrator.
refs: Chapter 1, 'What Management Is', section 1.3 'Resources and Results' — resources and results, the basis of the three measures; Chapter 8, 'Organising: Process and Structure', section 8.2 'The Organising Process' — how the levels become a formal structure; Chapter 11, 'Leadership', section 11.1 'Leadership and Management Compared' — how leading differs from managing at every level
need: Chapter 1, 'What Management Is', section 1.2 'Defining Management' and section 1.3 'Resources and Results'
ladder: Rung 1: a small tailoring shop with an owner and two helpers (levels and skills by name). Rung 2: a school with head, department heads and teachers, to find the three levels. Rung 3: a hospital ward in another country, using the three measures. Rung 4: a bus company where a manager must be effective but not efficient, and the reverse, in the same month.
practice: review: place named job titles on the three levels, explain which skill matters most at each level and why, show with a made-up shop the difference between productivity and efficiency, give one reason for and one against calling management a profession; think: a clinic improves its output but reaches fewer patients in need, and the reader says which measure is weak; pause: after the three skills and after the three measures.
sources: yes

=== CH03 ===
title: How Management Thought Developed
purpose: Trace how ideas about managing developed, so that the reader can recognise each approach and judge when it still helps.
pace: slow — foundation chapter; many named thinkers, each idea opposed to the one before
style: descriptive
words: 4825
figures: 1
- fig01: a timeline of five approaches to managing, with the period of each and its main idea
plate: a mill floor with a timekeeper holding a pocket watch beside a loom, 1880s
sections:
3.1 | Early Ideas and Scientific Management | new idea | 775
3.2 | Fayol and Administrative Principles | framework | 550
3.3 | Human Relations and Behavioural Thought | new idea | 225
3.4 | Management Science, Systems and Contingency | new idea | 675
concepts:
- 3.1 | Why early industry needed new methods | standard | needs: none
- 3.1 | Scientific management | core | needs: why early industry needed new methods
- 3.2 | Fayol's administrative principles | core | needs: scientific management
- 3.3 | Human relations and behavioural thought | standard | needs: fayol's administrative principles
- 3.4 | Management science approach | standard | needs: scientific management
- 3.4 | Systems approach | standard | needs: human relations and behavioural thought
- 3.4 | Contingency approach | standard | needs: systems approach
defines:
- Scientific management | a method that studies each task by measurement, finds the best way to do it and trains employees in that way
- Time study | the careful timing of each step of a task to find out how long the work should take
- Administrative management | a view that studies the whole organisation and seeks general principles for managing it
- Principle of management | a general guide to good managing, which is tested by use and is not a law of nature
- Division of work | the splitting of a large task into smaller tasks, each done by one person or group
- Unity of command | the rule that each employee receives orders from one manager only
- Scalar chain | the line of authority from the top of an organisation down to the lowest level
- Human relations approach | a view that output depends on the needs, feelings and groups of employees as well as on methods
- Behavioural approach | the study of how individuals and groups act at work, using methods from psychology and sociology
- Management science approach | the use of mathematical models and measured data to solve managerial problems
- System | a set of connected parts that work together and receive inputs from, and give outputs to, their surroundings
- Contingency approach | the view that the best way to manage depends on the situation
assumes: Management; Manager; Management function; Management process; Productivity; Efficiency
words-in-use: method, rule
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; 13 employees and the owner at 1 December 2025. Time study of 10 November 2025 (by Imran Meghna): packing a parcel of three books, ten parcels timed for each of three methods; averages per parcel: method A 9 minutes, method B 7 minutes, method C 6 minutes. Method C was adopted on 1 December 2025; the orders and parcels section packs 40 parcels each day, so the saving is 3 minutes x 40 = 120 minutes each day against method A. Conflicting orders on 15 December 2025: a shop assistant received different orders from the stationery section leader and from the shop floor manager at the same time; shelving of 300 items was delayed by 2 hours; from 16 December 2025 each assistant receives orders from one section leader only. Reorder rule of 20 December 2025 (Rubel Hossain): a school notebook sells 60 a day and delivery takes 5 days, so the shop reorders when stock falls to 300 notebooks. The same rule is not used in the January rush, when daily sales are higher.
history: Frederick W. Taylor's work at Bethlehem Steel, Pennsylvania, 1898 to 1901, on handling pig iron and on shovelling, and the criticism it met; use only facts that sources agree on and date every figure. Search hint: Taylor Bethlehem Steel 1899 pig iron scientific management.
refs: Chapter 2, 'Managers: Levels, Skills and Standing', section 2.3 'Productivity, Effectiveness and Efficiency' — the efficiency that scientific management sought; Chapter 9, 'Span, Departments, Authority and Coordination', section 9.3 'Authority, Responsibility and Delegation' — authority and unity of command in practice; Chapter 10, 'People, Motivation and Creativity', section 10.1 'Human Factors and Assumptions about People' — the human assumptions that behavioural thought brought forward
need: Chapter 2, 'Managers: Levels, Skills and Standing', section 2.3 'Productivity, Effectiveness and Efficiency'
ladder: Rung 1: a farmer timing two ways of planting a row (scientific management). Rung 2: a school office where two heads give orders to one clerk (unity of command). Rung 3: a call centre in another country that applies each approach in turn. Rung 4: a bus depot that needs time study, clear authority, attention to drivers and a contingency view together.
practice: review: match everyday work situations to the five approaches, explain what a principle of management is and is not, give one limit of scientific management, say what a contingency view adds to a fixed list of principles; think: a bakery uses a time study and the bakers stop speaking to the owner, and the reader names what was missing; pause: after scientific management and after the contrast of human relations with it.
sources: yes

=== CH04 ===
title: Environment, Ethics and Social Responsibility
purpose: Show how forces outside and inside an organisation affect a manager's work, how managers respond, and what society expects in return.
pace: standard — five sections; the social and ethical ideas are new but concrete
style: descriptive
words: 4800
figures: 2
- fig01: an organisation drawn inside two rings: the internal environment and the external forces around it
- fig02: the groups of stakeholders drawn around one organisation, with what each expects
plate: a harbour quay with ships, warehouses and a weather vane, 1870s
sections:
4.1 | Internal and External Environment | new idea | 325
4.2 | Forces in the External Environment | framework | 550
4.3 | Managing and Adapting to the Environment | technique | 450
4.4 | Social Responsibility and Sustainability | defining theory | 550
4.5 | Business Ethics | new idea | 325
concepts:
- 4.1 | Environment of an organisation | standard | needs: management defined
- 4.1 | Internal and external environment compared | minor | needs: environment of an organisation
- 4.2 | Economic, social, political, legal and technological forces | core | needs: internal and external environment compared
- 4.3 | Scanning the environment | standard | needs: economic, social, political, legal and technological forces
- 4.3 | Responding and adapting | standard | needs: scanning the environment
- 4.4 | Social responsibility and stakeholders | standard | needs: responding and adapting
- 4.4 | Davis's view of responsibility and power | standard | needs: social responsibility and stakeholders
- 4.4 | Sustainability | minor | needs: social responsibility and stakeholders
- 4.5 | Ethics in business | standard | needs: social responsibility and stakeholders
- 4.5 | Ethical conduct and ethical codes | minor | needs: ethics in business
defines:
- Environment | all the forces, inside and outside an organisation, that can affect how it works and what it achieves
- Internal environment | the people, structure, rules and resources inside an organisation that a manager can change directly
- External environment | the forces outside an organisation that affect it and that a manager cannot control directly
- Economic force | a condition of money, prices, income and trade that affects an organisation
- Social force | a change in the habits, values, numbers or beliefs of people that affects an organisation
- Political and legal force | a government decision, law or rule that affects what an organisation may or must do
- Technological force | a new tool, machine or method that changes how work is done or what is sold
- Environmental scanning | the steady collection and study of information about outside forces so that changes are seen early
- Stakeholder | a person or group affected by what an organisation does, such as owners, employees, customers and neighbours
- Corporate social responsibility | the duty of an organisation to act for the good of society as well as for its own gain
- Sustainability | the use of resources in a way that does not harm the ability of later generations to meet their needs
- Business ethics | the standards of right and wrong that guide how an organisation and its managers behave
assumes: Organisation; Resource; Manager; Management; Productivity; Efficiency
words-in-use: power (in Davis: influence on society), interest (in stakeholder), force
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; 2025 profit Tk 1,240,000; 13 employees and the owner. Economic: paper cost rose 12% between 1 July 2025 and 1 January 2026; a notebook that cost Tk 80 now costs Tk 89.60; the shop raised the selling price from Tk 100 to Tk 108 (8%) on 1 January 2026. Political and legal: the shop recorded on 15 December 2025 that a revised school curriculum is announced for the 2027 school year, which means new titles for school books. Social: in December 2025, 3 of every 10 customer enquiries (30%) asked for home delivery. Technological: mobile payment was introduced on 1 October 2025; in December 2025, 22% of sales were paid this way. Social responsibility: on 15 January 2026 the shop gave 2% of the 2025 profit, Tk 24,800, to a school library. Sustainability: from 1 March 2026 paper bags replace plastic bags; 30,000 bags are used in a year; a plastic bag costs Tk 1.50 and a paper bag Tk 4.00; the extra cost is Tk 75,000 a year. Ethics: on 11 November 2025 a distributor offered Imran Meghna a personal cash payment of Tk 40,000 for placing a larger order; he refused and reported it to the owner the same day.
history: The collapse of the Rana Plaza building in Savar, Bangladesh, on 24 April 2013, and the Accord on Fire and Building Safety in Bangladesh, signed from 15 May 2013: a case of social responsibility in a supply chain. Use only dated, widely reported facts and avoid figures that sources dispute. Search hint: Rana Plaza 24 April 2013 Accord on Fire and Building Safety.
refs: Chapter 5, 'Planning', section 5.3 'The Planning Process' — the premises that planning takes from the environment; Chapter 7, 'Decision Making', section 7.2 'Elements and Conditions of a Decision' — decisions under risk and uncertainty; Chapter 12, 'Controlling', section 12.4 'Requirements and Barriers' — barriers that arise from outside forces
need: Chapter 1, 'What Management Is', section 1.1 'Why Organisations Need Management' and section 1.3 'Resources and Results'
ladder: Rung 1: a roadside fruit seller facing a rise in the price of fuel (economic force). Rung 2: a school facing a change of rule from the education authority (political and legal force). Rung 3: a clothing exporter in another country facing new buyer rules (all five forces and stakeholders). Rung 4: a bus company deciding on cleaner vehicles, with cost, law, ethics and community expectations combined.
practice: review: sort a set of news items into the five forces, name the stakeholders of a named organisation and what each expects, explain how sustainability differs from profit, give a case where a legal act might still be unethical; think: an owner is offered a cheaper supplier whose factory is unsafe, and the reader weighs the stakeholders; pause: after the five forces and after the four responsibilities in Davis.
sources: yes

=== CH05 ===
title: Planning
purpose: Teach planning as the first management function: what a plan is, the types of plan, the steps of the planning process and why plans fail or succeed.
pace: standard — descriptive; the process is sequential and concrete
style: descriptive
words: 4725
figures: 2
- fig01: the steps of the planning process in order, with the feedback line from review back to the premises
- fig02: standing plans and single-use plans shown as two branches with their parts
plate: a draughtsman at a drawing board with plans and a T-square, 1880s
sections:
5.1 | Meaning, Nature and Purpose | new idea | 675
5.2 | Types of Plans | framework | 225
5.3 | The Planning Process | technique | 775
5.4 | Limits and Effectiveness | new idea | 450
concepts:
- 5.1 | What planning is | standard | needs: management defined
- 5.1 | Nature of planning | standard | needs: what planning is
- 5.1 | Purposes of planning | standard | needs: what planning is
- 5.2 | Standing plans and single-use plans | standard | needs: what planning is
- 5.3 | Planning premises | standard | needs: nature of planning; economic, social, political, legal and technological forces
- 5.3 | Steps of the planning process | core | needs: planning premises
- 5.4 | Limits of planning and why plans fail | standard | needs: steps of the planning process
- 5.4 | Making planning effective | standard | needs: limits of planning and why plans fail
defines:
- Planning | choosing in advance what the organisation will do and how it will do it
- Plan | a written or agreed description of what is to be done, by whom, by when and with what resources
- Planning premise | an assumption about the future conditions under which a plan will be carried out
- Standing plan | a plan made once and used again and again for situations that recur
- Single-use plan | a plan made for one occasion or project that is not used again in the same form
- Policy | a standing plan that gives a general guide for decisions without fixing the exact action
- Procedure | a standing plan that sets out the steps to be followed for a recurring task, in order
- Rule | a standing plan that requires or forbids one specific action, with no choice
- Programme | a single-use plan that sets out the steps, order, timing and resources for a set of related tasks
- Budget | a plan stated in money, or in other numbers, for a period of time
assumes: Management; Manager; Management function; Resource; Economic force; Social force; Political and legal force; Technological force; Environmental scanning
words-in-use: plan (the verb and the noun), premise
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna. Planning meeting of 6 January 2026. Result for 2025: sales Tk 18,600,000. Sales objective for 2026: Tk 20,460,000, which is 10% above 2025. Premises recorded: paper cost up 12% between 1 July 2025 and 1 January 2026; school enrolment unchanged; rent unchanged at Tk 200,000 per month; employee pay up 5% from 1 January 2026, so yearly pay for the 13 employees rises from Tk 5,100,000 to Tk 5,355,000. Alternatives listed: longer opening hours; online ordering; a second branch; no change. Online ordering and the second branch were carried forward for study. Standing plans in use: policy, books in good condition are exchanged within 7 days; procedure, four steps for receiving new stock; rule, no stock leaves the shop without a record. Single-use plan: the January school-term rush programme of 1 to 31 January 2026, with extra stock of Tk 900,000 ordered on 10 December 2025. A failed plan of 2024: 1,200 copies of one guide book were ordered on the premise that the school curriculum would not change; it was revised three months later; 400 copies sold; 800 unsold copies at Tk 180 each, Tk 144,000, were written off.
history: Eastman Kodak: its engineer Steven Sasson built a digital camera in 1975, the company's plans kept its film business at the centre, and Kodak filed for bankruptcy protection on 19 January 2012. Use only dated facts that sources agree on. Search hint: Kodak digital camera 1975 Sasson bankruptcy 19 January 2012.
refs: Chapter 4, 'Environment, Ethics and Social Responsibility', section 4.2 'Forces in the External Environment' — outside forces that supply premises; Chapter 6, 'Objectives and Management by Objectives', section 6.1 'Nature of Objectives' — objectives that every plan serves; Chapter 7, 'Decision Making', section 7.1 'The Decision-Making Process' — choosing among alternatives; Chapter 12, 'Controlling', section 12.5 'Control and Planning Together' — how control feeds back into plans
need: Chapter 4, 'Environment, Ethics and Social Responsibility', section 4.2 'Forces in the External Environment' and section 4.3 'Managing and Adapting to the Environment'
ladder: Rung 1: a family planning a wedding day (premises and steps). Rung 2: a school planning an annual sports day, split into standing and single-use parts. Rung 3: a farm cooperative in another country planning a harvest under weather risk. Rung 4: a clothing shop planning a new season, using premises, alternatives, review and the limits of planning together.
practice: review: say in new words the six steps of the planning process in order, sort named plans into standing and single-use, explain the role of a premise with a new example, name two reasons a plan can fail; think: a bakery plans a new branch on premises that prove wrong, and the reader finds the wrong premise and revises the plan; pause: after premises and after the planning steps.
sources: no

=== CH06 ===
title: Objectives and Management by Objectives
purpose: Show what objectives are, how they are set in the key areas of an organisation, how management by objectives works as a cycle, and where it helps or hinders.
pace: standard — descriptive; one cycle and one list of areas
style: descriptive
words: 4375
figures: 2
- fig01: the hierarchy of objectives from the whole organisation down to one employee
- fig02: the cycle of management by objectives as a loop of five steps
plate: a surveyor sighting through a theodolite toward a distant flag, 1870s
sections:
6.1 | Nature of Objectives | new idea | 325
6.2 | Setting Objectives | framework | 450
6.3 | The MBO Cycle | technique | 775
6.4 | Benefits and Weaknesses of MBO | new idea | 225
concepts:
- 6.1 | What an objective is | standard | needs: planning defined; plan
- 6.1 | Hierarchy of objectives | minor | needs: what an objective is
- 6.2 | Setting objectives: the qualities of a good one | standard | needs: what an objective is
- 6.2 | Eight key areas for objectives | standard | needs: setting objectives: the qualities of a good one
- 6.3 | Management by objectives defined | standard | needs: hierarchy of objectives
- 6.3 | The cycle of management by objectives | core | needs: management by objectives defined
- 6.4 | Benefits and weaknesses of management by objectives | standard | needs: the cycle of management by objectives
defines:
- Objective | a result, stated clearly and with a time limit, that an organisation or person aims to reach
- Hierarchy of objectives | the arrangement of objectives from the whole organisation down to departments and individuals, each supporting the one above
- Key area | one of the main parts of an organisation where results must be set because they decide its success
- Management by objectives | a way of managing in which managers and employees agree objectives together and judge performance against them
- Performance review | a meeting held at a set time to compare results with objectives and to agree what to do next
- Participation | the sharing of a decision between a manager and the employees who must carry it out
assumes: Planning; Plan; Planning premise; Budget; Management function; Employee
words-in-use: objective (formal sense), review
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; objectives set on 7 January 2026 for the year to 31 December 2026, in eight key areas. Base figures for 2025: sales Tk 18,600,000; school books 60% of sales, Tk 11,160,000; profit Tk 1,240,000; unsold stock written off Tk 186,000; cash reserve Tk 1,500,000; 2 of 13 employees left in 2025 (15.4%); gift to a school library Tk 24,800 (2% of profit). Objectives: market standing, school-book sales to Tk 12,276,000 (10% more); innovation, decide on online ordering by 31 January 2026 and, if approved, begin by 30 June 2026; productivity, stock written off below Tk 150,000; physical and financial resources, cash reserve to Tk 1,800,000; profitability, profit Tk 1,500,000; manager performance and development, each of the 3 managers completes one training course by 30 November 2026; employee performance and attitude, at most 1 of 13 employees leaves in 2026 (7.7%); public responsibility, a gift of 2% of 2026 profit, Tk 30,000. Cycle: objectives agreed with each manager by 15 January 2026; review on 30 June 2026 and on 31 December 2026. Record of a weakness: by 15 January 2026 the sales objective had been written in full for every manager and the service objective for none.
history: Peter F. Drucker, The Practice of Management (1954), which named management by objectives, and the objectives that Hewlett-Packard set in 1957; use only dated facts that sources agree on. Search hint: Drucker 1954 management by objectives; Hewlett-Packard objectives 1957.
refs: Chapter 5, 'Planning', section 5.1 'Meaning, Nature and Purpose' — planning as the source of objectives; Chapter 7, 'Decision Making', section 7.1 'The Decision-Making Process' — decisions that carry objectives out; Chapter 12, 'Controlling', section 12.2 'The Control Process' — measuring results against standards
need: Chapter 5, 'Planning', section 5.1 'Meaning, Nature and Purpose' and section 5.3 'The Planning Process'
ladder: Rung 1: a student setting objectives for one term (qualities of a good objective). Rung 2: a school library with objectives in several key areas. Rung 3: a hospital in another country applying the cycle to a ward. Rung 4: a small factory where objectives conflict across key areas and the cycle must settle the conflict.
practice: review: rewrite a vague aim as a clear objective with a time limit, name the eight key areas with an example of each, put the five steps of the cycle in order for a new organisation, give two benefits and two weaknesses of the method; think: a bakery sets a sales objective only and quality falls, and the reader names the missing key area; pause: after the cycle and after the weaknesses.
sources: yes

=== CH07 ===
title: Decision Making
purpose: Teach decision making as a process with named elements and conditions, show how groups and real limits shape it, and give the reader the tools of probability and decision trees.
pace: slow — expected value and decision trees are new, abstract and have several moving parts
style: mixed
words: 5150
figures: 2
- fig01: the steps of the rational decision-making process as a flow with a return path
- fig02: a decision tree with two options, chance branches, probabilities and expected values
plate: a pair of brass scales on a counting-house table with coins and a quill, 1880s
sections:
7.1 | The Decision-Making Process | framework | 550
7.2 | Elements and Conditions of a Decision | framework | 775
7.3 | Groups and Real-World Constraints | new idea | 550
7.4 | Tools: Probability, Decision Trees and Support Systems | technique | 675
concepts:
- 7.1 | Steps of the rational decision-making process | core | needs: planning defined; objective
- 7.2 | Elements of a decision situation | standard | needs: steps of the rational decision-making process
- 7.2 | Certainty, risk and uncertainty | core | needs: elements of a decision situation
- 7.3 | Nature of managerial decision making and its limits | standard | needs: steps of the rational decision-making process
- 7.3 | Group decision making: gains and costs | standard | needs: nature of managerial decision making and its limits
- 7.3 | Other influences on a decision | minor | needs: group decision making: gains and costs
- 7.4 | Probability and expected value | standard | needs: certainty, risk and uncertainty
- 7.4 | Decision trees | standard | needs: probability and expected value
- 7.4 | Decision support systems | standard | needs: decision trees
defines:
- Decision | a choice made between two or more alternatives to reach an aim
- Decision making | the process of recognising a problem or chance, finding alternatives and choosing one
- Decision maker | the person or group that makes the choice
- Alternative | one of the possible courses of action from which a choice is made
- Criterion | a standard used to judge the alternatives, such as cost or risk
- Certainty | a condition in which the decision maker knows the result of each alternative
- Risk | a condition in which the result of each alternative is not known but its probability is known
- Uncertainty | a condition in which neither the result nor the probability of each alternative is known
- Rational decision making | choosing the alternative that best meets set criteria after studying all the alternatives
- Bounded rationality | the limit on rational choice that arises because people have limited time, information and ability
- Groupthink | the habit of a close group to agree quickly and to ignore doubts and facts that disturb agreement
- Probability | a number between 0 and 1 that states how likely an event is
- Expected value | the sum of each possible result multiplied by its probability
- Decision tree | a diagram that shows alternatives, chance events, probabilities and results in branches
- Decision support system | a computer-based set of data and tools that helps a manager study a decision
assumes: Management; Manager; Planning; Plan; Objective; Resource; Management by objectives
words-in-use: decision, risk, value
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna. Meeting of 20 January 2026 (95 minutes; the owner and 3 managers). Cash reserve Tk 1,500,000. Problem: sales growth of 10% (Tk 20,460,000) cannot come from walk-in customers alone. Alternatives: A, open a second branch, cost Tk 2,400,000 (Tk 900,000 more than the cash reserve); B, begin online ordering, cost Tk 600,000; C, change nothing. Criteria: cost within the cash reserve; expected value over three years; risk. Demand, with probabilities: branch, strong 0.5 giving extra profit Tk 1,200,000 a year, weak 0.5 giving Tk 200,000 a year; online, strong 0.6 giving Tk 700,000 a year, weak 0.4 giving Tk 150,000 a year. Expected profit a year: A Tk 700,000; B Tk 480,000. Over three years: A Tk 2,100,000, less cost Tk 2,400,000, net Tk -300,000; B Tk 1,440,000, less cost Tk 600,000, net Tk 840,000; C Tk 0. Before the meeting 2 of the 4 favoured the branch; after it all 4 favoured online ordering. Rent Tk 200,000 a month is a certain figure; the 2027 curriculum is an uncertain one. Data came from a sales spreadsheet covering two years only. Decision recorded on 21 January 2026: begin online ordering.
history: The decision to launch the space shuttle Challenger on 28 January 1986 and the findings of the Rogers Commission (1986); group pressure and the handling of risk. Use only dated facts that sources agree on. Search hint: Challenger launch decision 28 January 1986 Rogers Commission.
refs: Chapter 4, 'Environment, Ethics and Social Responsibility', section 4.3 'Managing and Adapting to the Environment' — risk from outside forces; Chapter 5, 'Planning', section 5.3 'The Planning Process' — choosing among alternatives in the planning process; Appendix A1, 'Maths You Will Use', section A1.1 'Percentages and Percentage Change' — percentages and probability as a share; Appendix A1, 'Maths You Will Use', section A1.3 'Rearranging an Equation' — rearranging a formula for expected value
need: Chapter 5, 'Planning', section 5.3 'The Planning Process' and Chapter 6, 'Objectives and Management by Objectives', section 6.1 'Nature of Objectives'
ladder: Rung 1: choosing between two bus routes with certain times (steps and certainty). Rung 2: a stall owner choosing between two spots with a probability of rain (risk and expected value, clean numbers). Rung 3: a farm in another country choosing a crop with uncertain weather (decision tree with messier numbers). Rung 4: a company choosing among three projects, using a tree, a group meeting and the limits of rational choice together.
practice: review: put the steps in order for a new decision, sort named cases into certainty, risk and uncertainty, work out an expected value from new data, explain one gain and one cost of a group decision; think: two projects with different costs and chances, and the reader draws the tree and decides; pause: after expected value and after the first decision tree.
sources: no

=== CH08 ===
title: Organising: Process and Structure
purpose: Teach organising as the function that turns plans into a working structure: its steps, formal and informal parts, the forces that shape structure and two models of design.
pace: standard — descriptive; many structure terms but each is concrete
style: descriptive
words: 4950
figures: 2
- fig01: an organisation chart of a small firm showing levels and lines of reporting
- fig02: formal and informal organisation drawn as two overlapping sets of relationships
plate: a railway station with a signal box and a clerk with a timetable board, 1880s
sections:
8.1 | Meaning, Nature and Purpose | new idea | 675
8.2 | The Organising Process | technique | 225
8.3 | Formal and Informal Organisation | framework | 225
8.4 | Structure and the Forces Behind It | framework | 450
8.5 | Design Models and Situational Factors | defining theory | 775
concepts:
- 8.1 | What organising is | standard | needs: planning defined; plan
- 8.1 | Nature of organising | standard | needs: what organising is
- 8.1 | Purposes of organising | standard | needs: what organising is
- 8.2 | Steps of the organising process | standard | needs: division of work; what organising is
- 8.3 | Formal and informal organisation | standard | needs: steps of the organising process
- 8.4 | Organisation structure and the organisation chart | standard | needs: steps of the organising process
- 8.4 | Forces that shape structure | standard | needs: organisation structure and the organisation chart
- 8.5 | Bureaucratic and behavioural models of design | core | needs: forces that shape structure; scientific management
- 8.5 | Situational factors in design | standard | needs: bureaucratic and behavioural models of design
defines:
- Organising | arranging the work, people and resources of an organisation so that plans can be carried out
- Organisation chart | a diagram that shows the parts of an organisation, the levels and who reports to whom
- Organisation structure | the way in which the tasks, people and lines of reporting of an organisation are arranged
- Formal organisation | the structure that is officially set by management, with defined tasks and lines of reporting
- Informal organisation | the network of personal relationships among employees that arises on its own and is not on the chart
- Line organisation | a structure in which authority passes in one straight line from the top to the bottom
- Line-and-staff organisation | a structure in which line managers direct the main work and staff specialists advise them
- Organisation design | the choice of the structure that best fits the aims, size, work and surroundings of an organisation
- Bureaucratic model | a design with fixed rules, clear levels, written records and promotion by set standards
- Behavioural model | a design that gives weight to the needs, skills and participation of employees and uses fewer fixed rules
- Situational factor | a feature of an organisation or its surroundings, such as size or technology, that affects which design fits best
assumes: Management; Manager; Management function; Planning; Plan; Division of work; Unity of command; Scalar chain; Scientific management; Human relations approach; Contingency approach; Top manager; Middle manager; First-line manager
words-in-use: organisation, structure, line
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna. Organising record of 1 March to 1 April 2026, after the decision of 21 January 2026 to begin online ordering. Work listed: buying; selling in the shop; orders and parcels; accounts; online sales. Structure at 1 March 2026 (14 people): owner; three managers (Imran Meghna, purchasing, with 1 assistant; Nasrin Akter, shop floor; Rubel Hossain, accounts, with 1 assistant); four section leaders under Nasrin Akter (school books with 2 assistants; general books with 1; stationery with 1; orders and parcels with none). Rule in force: every purchase order above Tk 20,000 needs the owner's signature. Informal organisation: since 2024 five employees (two section leaders and three assistants) cover one another's shifts by agreement, which is not on the chart. From 1 April 2026 three people join: Farhan Meghna as online manager at Tk 55,000 a month, and two online assistants at Tk 22,000 a month each; extra pay Tk 99,000 a month, Tk 1,188,000 a year; total 17 people. Situational factors recorded: size grew from 14 to 17; a website was added; the 2027 curriculum change is expected. Design in use: mostly bureaucratic (written rules, signatures), with more discretion for section leaders on shelf layout.
history: Daniel C. McCallum, general superintendent of the New York and Erie Railroad, and the organisation chart drawn for it in 1855, to deal with long lines and many employees. Use only dated facts that sources agree on. Search hint: McCallum Erie Railroad 1855 organisation chart.
refs: Chapter 3, 'How Management Thought Developed', section 3.2 'Fayol and Administrative Principles' — Fayol on unity of command and the scalar chain; Chapter 9, 'Span, Departments, Authority and Coordination', section 9.1 'Span of Management' — how many subordinates one manager can direct; Chapter 9, 'Span, Departments, Authority and Coordination', section 9.3 'Authority, Responsibility and Delegation' — authority along the lines of the chart; Chapter 10, 'People, Motivation and Creativity', section 10.3 'Informal Groups and Teams' — informal groups in more detail
need: Chapter 3, 'How Management Thought Developed', section 3.2 'Fayol and Administrative Principles' and Chapter 5, 'Planning', section 5.2 'Types of Plans'
ladder: Rung 1: a family-run tea garden (steps of organising, drawn as a chart). Rung 2: a school with an informal staff group that the chart omits. Rung 3: a bank branch in another country compared under the bureaucratic and behavioural models. Rung 4: a growing firm that must change its design as size, technology and surroundings change together.
practice: review: draw a chart from a short description, name the steps of organising in order, separate formal from informal parts in a new case, contrast the two design models with one advantage and one limit each; think: a workshop doubles in size and the old design stops working, and the reader names the situational factor at fault; pause: after the organising steps and after the two models.
sources: yes

=== CH09 ===
title: Span, Departments, Authority and Coordination
purpose: Teach how work is divided and grouped, how many people one manager can direct, how authority is shared and delegated, and how the parts are coordinated.
pace: standard — descriptive; several similar terms, each separated by an example
style: descriptive
words: 4625
figures: 2
- fig01: a tall structure and a flat structure for the same 17 people, drawn side by side
- fig02: authority and decision rights shown on a line from centralised to decentralised
plate: a lattice-girder bridge over a river with several spans, 1880s
sections:
9.1 | Span of Management | new idea | 450
9.2 | Departmentalisation | framework | 225
9.3 | Authority, Responsibility and Delegation | framework | 675
9.4 | Centralisation and Decentralisation | new idea | 225
9.5 | Coordination | technique | 450
concepts:
- 9.1 | Span of management | standard | needs: organisation structure
- 9.1 | Factors that decide the span | standard | needs: span of management
- 9.2 | Departmentalisation | standard | needs: division of work; organisation structure
- 9.3 | Authority, responsibility and accountability | standard | needs: scalar chain
- 9.3 | Line, staff and functional authority | standard | needs: authority, responsibility and accountability
- 9.3 | Delegation and its obstacles | standard | needs: authority, responsibility and accountability
- 9.4 | Centralisation and decentralisation | standard | needs: delegation and its obstacles
- 9.5 | Coordination and why divided work needs it | standard | needs: departmentalisation
- 9.5 | Structural and activity coordination | standard | needs: coordination and why divided work needs it
defines:
- Span of management | the number of subordinates who report directly to one manager
- Tall structure | a structure with many levels and a narrow span of management at each level
- Flat structure | a structure with few levels and a wide span of management at each level
- Departmentalisation | the grouping of jobs into departments by a common feature such as function, product, area or customer
- Authority | the right of a manager to make decisions and to direct others, given by the position held
- Responsibility | the duty to carry out the tasks assigned and to answer for the results
- Accountability | the obligation to report on results and to accept the consequences
- Line authority | the right to direct the work of subordinates in the main chain of command
- Staff authority | the right to advise and serve line managers without directing their subordinates
- Functional authority | the limited right of a specialist to direct others in one matter that falls in his or her field
- Delegation | giving a subordinate the authority to carry out a task while the manager remains answerable for the result
- Centralisation | keeping most decision-making authority at the top of an organisation
- Decentralisation | passing decision-making authority down to lower levels
- Coordination | joining the work of different people and parts so that they act together towards the same aim
assumes: Organising; Organisation chart; Organisation structure; Formal organisation; Informal organisation; Line organisation; Line-and-staff organisation; Division of work; Unity of command; Scalar chain; Top manager; Middle manager; First-line manager; Functional manager; Situational factor
words-in-use: span, authority, line
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; structure from 1 April 2026 (17 people): owner; four managers (Imran Meghna, purchasing, 1 assistant; Nasrin Akter, shop floor; Rubel Hossain, accounts, 1 assistant; Farhan Meghna, online, 2 assistants); four section leaders under Nasrin Akter (school books with 2 assistants; general books with 1; stationery with 1; orders and parcels with none). Spans: owner 4; Nasrin Akter 4; Farhan Meghna 2; Imran Meghna 1; Rubel Hossain 1. Grouping: by function (purchasing, shop floor, accounts, online); inside the shop floor, by product (school books, general books, stationery) and by process (orders and parcels). Rubel Hossain also holds functional authority over spending forms in every section. Delegation on 1 April 2026: the owner moves the approval of purchase orders up to Tk 100,000 to Imran Meghna (it was Tk 20,000 before); larger orders still need the owner's signature; the owner remains answerable for purchasing results; Imran reports on orders to the owner each month. Record for April 2026: 18 orders approved by Imran Meghna; 2 above Tk 100,000 went to the owner. Coordination: a Monday meeting of the four managers at 9:30 for 30 minutes; a stock list updated each day by 18:00; online parcels reach the orders and parcels section before 14:00.
history: General Motors in the 1920s: Alfred P. Sloan's organisation study of 1920 and the policy of decentralised operations with central control of finance and policy. Use only dated facts that sources agree on. Search hint: Alfred Sloan General Motors 1920 organisation study decentralisation.
refs: Chapter 8, 'Organising: Process and Structure', section 8.2 'The Organising Process' — the steps that lead to these choices; Chapter 8, 'Organising: Process and Structure', section 8.4 'Structure and the Forces Behind It' — structure and its forces; Chapter 11, 'Leadership', section 11.2 'Power and Authority Bases' — power, which differs from authority; Chapter 12, 'Controlling', section 12.3 'Types of Control' — control that suits each degree of decentralisation
need: Chapter 8, 'Organising: Process and Structure', section 8.2 'The Organising Process' and section 8.4 'Structure and the Forces Behind It'
ladder: Rung 1: a cricket club with a captain and ten players (span, authority). Rung 2: a college where a head delegates timetable work (delegation and its obstacles). Rung 3: a retail chain in another country that centralises buying but decentralises selling. Rung 4: a hospital whose span, grouping, authority and coordination must change together after a merger.
practice: review: count the span at each level of a drawn structure, say how a flat structure differs from a tall one, separate authority from responsibility with a new case, list the steps of delegation and one obstacle, name two ways to coordinate departments; think: a manager who delegates a task and then redoes it, and the reader names the fault and the fix; pause: after span of management and after delegation.
sources: no

=== CH10 ===
title: People, Motivation and Creativity
purpose: Teach what drives people at work: assumptions managers make about people, theories of motivation, the groups employees form and the conditions for creative work.
pace: standard — descriptive; theories are explained through the shop's records
style: descriptive
words: 4500
figures: 2
- fig01: the hierarchy of needs as a five-step staircase with an example of each step
- fig02: the needs-goal model as a loop from need to behaviour, goal and satisfaction
plate: a potter's workshop with workers at wheels and a master inspecting a vase, 1870s
sections:
10.1 | Human Factors and Assumptions about People | framework | 450
10.2 | Motivation | defining theory | 1000
10.3 | Informal Groups and Teams | new idea | 225
10.4 | Creativity and Innovation | new idea | 225
concepts:
- 10.1 | Human factors that affect management | standard | needs: human relations approach; behavioural approach
- 10.1 | Theory X and Theory Y | standard | needs: human factors that affect management
- 10.2 | Motivation and why managers must understand it | standard | needs: human factors that affect management
- 10.2 | The needs-goal model | standard | needs: motivation and why managers must understand it
- 10.2 | The hierarchy of needs | core | needs: the needs-goal model
- 10.3 | Informal groups and teams | standard | needs: informal organisation
- 10.4 | Creativity and innovation in an organisation | standard | needs: informal groups and teams
defines:
- Motivation | the inner force that starts, directs and keeps up a person's effort towards a goal
- Need | a lack of something that a person feels and wants to remove
- Needs-goal model | a model in which an unmet need creates a drive, the drive leads to behaviour, and reaching the goal satisfies the need
- Hierarchy of needs | Maslow's ordering of human needs in five levels, in which a lower level must be reasonably met before the next one matters
- Theory X | an assumption that people dislike work, avoid responsibility and must be directed and controlled
- Theory Y | an assumption that people can enjoy work, accept responsibility and direct themselves towards aims they share
- Informal group | a set of employees who join by personal choice for companionship, help or shared interest, and not by assignment
- Team | a small group of people with joint responsibility and complementary skills who work towards one common result
- Creativity | the ability to produce ideas that are new and useful
- Innovation | the use of a new idea in a product, a service or a method
assumes: Management; Manager; Employee; Informal organisation; Formal organisation; Human relations approach; Behavioural approach; Objective; Performance review; Participation
words-in-use: need, drive, theory
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; 13 employees and the owner; monthly pay Tk 22,000 for an assistant, Tk 32,000 for a section leader, Tk 55,000 for a manager. In 2025 two employees left: a school-books assistant who accepted Tk 25,000 a month elsewhere, and a section leader who gave no promotion path as the reason. Two practices recorded on 16 February 2026: a signing-in sheet every morning (Theory X) and permission for assistants to choose shelf layout inside their section (Theory Y). Needs record, 16 February 2026: pay and a monthly bonus (physical and safety needs); a written contract and a fixed holiday (safety); the lunch group and the Monday meeting (belonging); a monthly mention of the best section (esteem); a place on a training course (self-development). From 1 March 2026 each employee in a section that meets its monthly sales plan receives Tk 1,000. Informal group: five employees (two section leaders and three assistants) have eaten lunch together since 2024 and cover one another's shifts. Creativity: on 12 February 2026 an assistant proposed a Book of the Week shelf; trial from 2 March 2026; the featured titles sold 18 copies a week on average before and 31 after, an increase of 13 copies, 72%.
history: 3M under William L. McKnight: the 1948 rule that technical staff may spend part of their time on their own projects, and the Post-it note that grew from such work from 1974 to 1980. Use only dated facts that sources agree on. Search hint: 3M 15 percent time McKnight 1948 Post-it note history.
refs: Chapter 3, 'How Management Thought Developed', section 3.3 'Human Relations and Behavioural Thought' — human relations thought that these theories continue; Chapter 8, 'Organising: Process and Structure', section 8.3 'Formal and Informal Organisation' — informal organisation, the base of informal groups; Chapter 11, 'Leadership', section 11.4 'Styles and Modern Leadership' — leadership styles that go with each assumption
need: Chapter 3, 'How Management Thought Developed', section 3.3 'Human Relations and Behavioural Thought' and Chapter 8, 'Organising: Process and Structure', section 8.3 'Formal and Informal Organisation'
ladder: Rung 1: a student with a weak need for sleep and a strong need for marks (need and drive). Rung 2: a school office where Theory X and Theory Y give different results. Rung 3: a factory in another country using pay, team spirit and growth together. Rung 4: a design studio where needs, groups, creativity and a manager's assumptions interact.
practice: review: draw the needs-goal model for a new person, match examples to the five levels, contrast the two assumptions about people with an everyday case, explain why employees join informal groups, separate creativity from innovation; think: an employee refuses a bonus and the reader uses the hierarchy to say why; pause: after the hierarchy of needs and after Theory X and Theory Y.
sources: yes

=== CH11 ===
title: Leadership
purpose: Teach leadership as influence, how it differs from management, what gives a leader power, and how approaches, styles and modern forms of leadership are chosen and used.
pace: standard — descriptive; many named styles, each tied to one record
style: descriptive
words: 4400
figures: 2
- fig01: the leadership continuum from a manager who decides alone to a group that decides within limits
- fig02: five bases of power drawn as five roots of one tree, each with an example
plate: a ship's captain at the wheel on the bridge of a steamship, 1890s
sections:
11.1 | Leadership and Management Compared | new idea | 225
11.2 | Power and Authority Bases | framework | 225
11.3 | Trait, Situational and Continuum Approaches | framework | 675
11.4 | Styles and Modern Leadership | new idea | 675
concepts:
- 11.1 | Leadership and how it differs from management | standard | needs: management defined; manager
- 11.2 | Sources of power and how power differs from authority | standard | needs: authority; delegation
- 11.3 | Trait approach and situational approach | standard | needs: leadership and how it differs from management
- 11.3 | Styles of leadership | standard | needs: trait approach and situational approach
- 11.3 | The leadership continuum | standard | needs: styles of leadership
- 11.4 | Emotional intelligence of a leader | standard | needs: styles of leadership
- 11.4 | Transformational leadership | standard | needs: styles of leadership
- 11.4 | Coaching and super leadership | standard | needs: transformational leadership
defines:
- Leadership | the process of influencing people so that they work willingly towards a common aim
- Leader | a person who influences others to follow, whether or not he or she holds a managerial position
- Power | the ability to influence the behaviour of others, whether or not the right to do so is formally given
- Legitimate power | power that comes from the position a person holds in the organisation
- Reward power | power that comes from the ability to give things that others value
- Coercive power | power that comes from the ability to punish or to take away what others value
- Expert power | power that comes from special knowledge or skill that others need
- Referent power | power that comes from the respect and liking that others feel for a person
- Trait approach | the view that effective leaders are marked by certain personal qualities
- Situational approach | the view that effective leadership depends on the situation, including the task, the people and the setting
- Leadership style | the usual pattern of behaviour that a leader shows when influencing others
- Leadership continuum | a range of leader behaviour from full manager control to full control by the group, within limits
- Emotional intelligence | the ability to notice and manage one's own feelings and those of others and to use that awareness in dealing with people
- Transformational leadership | leadership that inspires followers to look beyond their own interest and to work for a shared vision
- Coaching | helping a person to improve skills through guidance, practice and feedback
- Super leadership | leadership that helps others to lead themselves
assumes: Management; Manager; Employee; Authority; Delegation; Theory X; Theory Y; Motivation; Informal group; Team
words-in-use: power, style, trait
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna; 13 employees and the owner (later 17). Continuum record: until 2025 the owner decided the opening hours and told the staff. On 5 February 2026 he put the question of closing at 20:00 or 21:00 to all 13 employees; 9 of 13 chose 21:00; the owner kept 21:00 for a trial of three months and set the review for 5 May 2026. Power record: legitimate, the owner's position; reward, the monthly Tk 1,000 section bonus; coercive, one written warning issued in 2025; expert, Imran Meghna's knowledge of publishers and supply; referent, Nasrin Akter, whom shop assistants consult first. Emotional intelligence record: on 24 February 2026 a customer complained about a wrong textbook edition; Nasrin Akter exchanged the book the same day and recorded the cause; no repeat in the next 30 days. Transformational leadership: on 2 March 2026 the owner issued a written aim to all employees: any book in Dhaka within 24 hours. Coaching: from 10 March 2026 Nasrin Akter held one hour a week with each of the 2 newest assistants. Super leadership: from 1 March 2026 the school-books section leader sets the weekly plan of her section without approval.
history: Ernest Shackleton and the Imperial Trans-Antarctic Expedition, 1914 to 1917: the loss of the Endurance and the return of all members of the party. Use only dated facts that sources agree on. Search hint: Shackleton Endurance 1914 1917 leadership all crew survived.
refs: Chapter 2, 'Managers: Levels, Skills and Standing', section 2.1 'Levels and Types of Managers' — managers at each level; Chapter 9, 'Span, Departments, Authority and Coordination', section 9.3 'Authority, Responsibility and Delegation' — authority, which differs from power; Chapter 10, 'People, Motivation and Creativity', section 10.1 'Human Factors and Assumptions about People' — Theory X and Theory Y, which match styles; Chapter 12, 'Controlling', section 12.3 'Types of Control' — control that suits a style of leadership
need: Chapter 9, 'Span, Departments, Authority and Coordination', section 9.3 'Authority, Responsibility and Delegation' and Chapter 10, 'People, Motivation and Creativity', section 10.1 'Human Factors and Assumptions about People'
ladder: Rung 1: a class monitor with no formal power (leader and manager apart). Rung 2: a football captain using the five bases of power. Rung 3: a head nurse in another country choosing a style for an emergency and for a quiet ward. Rung 4: a new manager who must choose a position on the continuum, a power base and a style for one team.
practice: review: separate a leader from a manager with a new example, match five cases to the five bases of power, place named decisions on the continuum, state when a style fits the situation, explain what coaching adds to telling; think: a team accepts every order and still fails to improve, and the reader names the missing form of leadership; pause: after the continuum and after power versus authority.
sources: yes

=== CH12 ===
title: Controlling
purpose: Teach controlling as the function that checks results against plans: its nature, the steps of the control process, three types of control and the conditions that make control succeed.
pace: standard — descriptive; one process and one set of three types
style: descriptive
words: 4375
figures: 2
- fig01: the control process as a loop of standard, measurement, comparison and corrective action
- fig02: three types of control placed on one timeline: before, during and after the work
plate: a steam engine with a governor and a pressure gauge on a mill floor, 1880s
sections:
12.1 | Meaning, Nature and Principles | new idea | 450
12.2 | The Control Process | technique | 550
12.3 | Types of Control | framework | 225
12.4 | Requirements and Barriers | new idea | 450
12.5 | Control and Planning Together | new idea | 100
concepts:
- 12.1 | What controlling is and its nature | standard | needs: management function
- 12.1 | Principles of controlling | standard | needs: what controlling is and its nature
- 12.2 | Steps of the control process | core | needs: plan; objective; standard
- 12.3 | Feedforward, concurrent and feedback control | standard | needs: steps of the control process
- 12.4 | Requirements of effective control | standard | needs: feedforward, concurrent and feedback control
- 12.4 | Barriers to successful control | standard | needs: requirements of effective control
- 12.5 | Control and planning together | minor | needs: steps of the control process; planning defined
defines:
- Controlling | measuring results, comparing them with standards and acting to correct differences
- Standard | a level of performance that is set in advance and used as the measure of actual results
- Deviation | the difference between actual results and the standard
- Corrective action | a change made to bring results back to the standard or to change the standard itself
- Feedforward control | control applied before work begins, to prevent a problem by checking inputs and plans
- Concurrent control | control applied while work is being done, to find and correct a problem at once
- Feedback control | control applied after work is finished, to learn from the results
- Monitoring | the regular watching of performance to see whether work is going as planned
assumes: Management; Manager; Management function; Management process; Planning; Plan; Objective; Management by objectives; Performance review; Delegation; Decentralisation; Authority; Leadership style
words-in-use: control, standard, measure
case: Case file, illustrative. Meghna and Sons, Dhanmondi, Dhaka; owner Harun Meghna. Sales objective for 2026: Tk 20,460,000. Monthly standard: Tk 1,705,000. Results: January 2026 Tk 1,610,000 (deviation Tk -95,000, -5.6%); February Tk 1,540,000 (Tk -165,000, -9.7%); March Tk 1,790,000 (Tk +85,000, +5.0%). First quarter: standard Tk 5,115,000; actual Tk 4,940,000; deviation Tk -175,000 (-3.4%). Stock write-off standard: Tk 150,000 a year, Tk 12,500 a month. Corrective action: the Book of the Week shelf (from 2 March 2026) was extended from one section to all three product sections on 15 March 2026. Feedforward: on 20 December 2025 the stock of the rush titles was checked against the order list before the January rush. Concurrent: a daily till count at 21:00 by the accounts assistant. Feedback: a monthly review on the 5th of the next month. Barriers recorded: the new daily till count form met resistance in the first two weeks; only sales, and not returns, were measured in January. Link to planning: the first-quarter deviation went to the plan review of 5 April 2026.
history: Barings Bank, Singapore and London: the collapse announced on 26 February 1995 after unauthorised trading by one employee and the failure to separate trading from settlement. Use only dated facts that sources agree on. Search hint: Barings Bank 26 February 1995 collapse Leeson internal controls.
refs: Chapter 5, 'Planning', section 5.4 'Limits and Effectiveness' — plans that need review and control; Chapter 6, 'Objectives and Management by Objectives', section 6.3 'The MBO Cycle' — the cycle of review in management by objectives; Chapter 9, 'Span, Departments, Authority and Coordination', section 9.4 'Centralisation and Decentralisation' — control in centralised and decentralised structures; Chapter 11, 'Leadership', section 11.3 'Trait, Situational and Continuum Approaches' — styles of leadership that fit different controls
need: Chapter 5, 'Planning', section 5.1 'Meaning, Nature and Purpose' and Chapter 6, 'Objectives and Management by Objectives', section 6.3 'The MBO Cycle'
ladder: Rung 1: a student checking monthly spending against a budget (standard, measure, correct). Rung 2: a school checking attendance with the three types of control. Rung 3: a power station in another country using control before, during and after a shutdown. Rung 4: a retail chain that must pick standards, measures and types of control together and meet barriers.
practice: review: put the control steps in order for a new case, calculate a deviation and its percentage from new figures, give one example of each type of control, name two barriers and a remedy for each, explain how control feeds back into planning; think: a shop meets its sales standard and loses customers, and the reader names the missing standard; pause: after the control steps and after the three types.
sources: no

=== A1 ===
title: Maths You Will Use
purpose: Give a short reference for the arithmetic used in this book: percentages, percentage change, ratios, averages, rounding, rearranging an equation and reading a graph.
pace: standard — reference, not a lesson
style: calculation
words: 950
figures: 1
- fig01: a simple line graph with labelled axes and one marked point, showing how to read a value from it
sections:
A1.1 | Percentages and Percentage Change | technique | 200
A1.2 | Ratios, Averages and Rounding | technique | 300
A1.3 | Rearranging an Equation | technique | 225
A1.4 | Reading a Graph | technique | 225
concepts:
- A1.1 | Percentage | minor | needs: none
- A1.1 | Percentage change | minor | needs: percentage
- A1.2 | Ratio | minor | needs: none
- A1.2 | Mean (average) | minor | needs: none
- A1.2 | Rounding | minor | needs: none
- A1.3 | Rearranging an equation | standard | needs: none
- A1.4 | Reading a graph | standard | needs: none
defines:
- Percentage | a number written as a part of 100, shown with the sign %
- Percentage change | the change between an old and a new value, divided by the old value and written as a percentage
- Ratio | a comparison of two quantities, shown as a:b or as a fraction
- Mean | the sum of a set of values divided by the number of values
- Rounding | replacing a number with a nearby number that has fewer digits, by a stated rule
- Axis | a labelled line on a graph along which a quantity is measured
assumes: none
words-in-use: average, rate
case: none
history: none
refs: none
need: nothing
ladder: Rung 1: a percentage of a simple price. Rung 2: a percentage change between two months of sales. Rung 3: a mean and a ratio from a short list. Rung 4: a formula rearranged, a result rounded and a value read from a graph, in one problem.
practice: review: five short items, one for each topic, with new numbers in taka; think: none; pause: none
sources: no

