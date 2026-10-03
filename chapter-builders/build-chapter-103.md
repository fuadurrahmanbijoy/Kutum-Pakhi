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
course: Accounting (MGT_103)
book: Accounting for Beginners
spelling: British · dates: day, month, year (12 March 2026) · country: mixed, no single country; the running case is in Bangladesh and the place is named whenever law or standards differ · currency and numbers: taka for the running case, written Tk 158,000 (international digit grouping); a historical case keeps its own currency
running case: Meghna and Sons — illustrative documented case file. Base facts (FIXED): Karim Meghna opened a binding and repair workshop in Mirpur, Dhaka, on 2 January 2022, helped by his sons Imran and Rafi, with Tk 600,000 of his own savings; the shop began selling books in 2022 and kept a service workshop; Imran became a partner on 1 January 2025; the business became Meghna Books Limited on 1 July 2026. Each chapter's entry holds its own figures.
chosen words (one term, one word):
- use balance sheet — also called statement of financial position
- use income statement — also called profit and loss account
- use owner's equity — also called capital, owner's capital
- use net income — also called net profit
- use cost of goods sold — also called cost of sales
- use non-current asset — also called fixed asset
- use plant asset — also called property, plant and equipment
- use temporary account — also called nominal account
- use permanent account — also called real account
- use account payable — also called creditor
- use account receivable — also called debtor
- use cash book — also called bank book (when it records only the bank account)
- use cheque — also called check
size plan: 18 chapters, ~80875 words, ~324 pages
chapters:
1. Business, Money and Records
2. Accounting, Its Users and Its Rules
3. The Accounting Equation
4. A First Look at the Financial Statements
5. Accounts, Debits and Credits
6. Journal and Ledger
7. The Trial Balance and the Accounting Cycle
8. Adjusting the Accounts
9. The Worksheet
10. Closing the Books
11. Merchandising Company Accounts and Classified Statements
12. Special Journals and the Cash Book
13. Bank Reconciliation
14. Inventory
15. Plant Assets and Depreciation
16. Non-Trading Concerns and Partnership Accounts
17. Partnership Liquidation
18. Company Accounting and Shares
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
title: Business, Money and Records
purpose: Show why a business needs written records and introduce the kinds of firm and ownership the book uses.
pace: standard — first chapter; it teaches how to read the book as well as the subject
style: descriptive
words: 4125
figures: 3
- fig01: a household month shown as money-in and money-out arrows
- fig02: the three kinds of firm side by side, with what each one sells
- fig03: three ownership forms as owner-and-business diagrams
plate: a shopkeeper at a lamplit counter beside a drawer of coins and a heap of loose paper slips, 1880s
sections:
1.1 | Everyday Money and the Need for Records | new idea | 550
1.2 | What Businesses Do | new idea | 325
1.3 | Service, Merchandising and Manufacturing Firms | framework | 325
1.4 | Sole Trader, Partnership and Company | framework | 325
concepts:
- 1.1 | Money in and money out | standard | needs: none
- 1.1 | Why we keep records | standard | needs: Money in and money out
- 1.1 | Memory is not a record | minor | needs: Why we keep records
- 1.2 | Business and its customers | standard | needs: none
- 1.2 | Profit and loss | minor | needs: Business and its customers
- 1.3 | Three kinds of firm | standard | needs: none
- 1.3 | Materials and finished goods | minor | needs: Three kinds of firm
- 1.4 | Three ways to own a business | standard | needs: none
- 1.4 | Who answers for what | minor | needs: Three ways to own a business
defines:
- Business | an organisation that provides goods or services to customers in order to earn money
- Profit | the money left over when a business has paid all its costs out of the money it earns
- Loss | the shortfall that results when a business's costs are greater than the money it earns
- Record | a written note, made at the time, of something that happened and its money value
- Customer | a person or organisation that pays for the goods or services a business provides
- Supplier | a person or organisation that sells goods or services to a business
- Owner | a person who put money into a business and has a claim on what is left after debts are paid
- Service firm | a business that earns money by doing work for customers instead of selling goods
- Merchandising firm | a business that buys finished goods and resells them without changing them
- Manufacturing firm | a business that makes goods from materials and then sells them
- Sole trader | one person who owns and runs a business and is personally responsible for its debts
- Partnership | a business owned by two or more people who agree to share its profit
- Company | a business that the law treats as a separate person, owned through shares
assumes: none
words-in-use: record; books
case: Meghna and Sons, illustrative. In December 2021 Karim Meghna, a bookbinder in Mirpur, Dhaka, decided to open a binding and repair workshop. On 2 January 2022 the workshop opened, with his sons Imran and Rafi helping. Until the end of the first week Karim kept loose notes in a shoebox: 31 paper slips, no dates on 9 of them. At the end of week 1 he could not tell whether the shop had earned a profit. Karim's own savings were the only money put into the business. No other figures are used in this chapter.
history: Clay tokens and tablets of ancient Sumer (about 3200 BC) used to record grain and livestock. Search: Uruk clay tablets earliest accounting records.
refs: Chapter 2, 'Accounting, Its Users and Its Rules', section 2.1 'What Accounting Is' — where record keeping becomes accounting
need: nothing
ladder: 1) a household's month of money in and out; 2) a market stall owner's shoebox; 3) the workshop in a new setting, a tailor's shop; 4) a case that combines the kind of firm with the form of ownership.
practice: review: sort new businesses into service, merchandising or manufacturing; name the ownership form from a short description; think: advise a friend who keeps all receipts in a bag how to start keeping records; pause: after 1.1 and after 1.4
sources: no

=== CH02 ===
title: Accounting, Its Users and Its Rules
purpose: Define accounting, name its branches and users, and explain why agreed rules exist.
pace: standard — vocabulary-heavy but each idea is small
style: descriptive
words: 4000
figures: 2
- fig01: the four jobs of accounting as a flow from event to report
- fig02: users of accounting information arranged around a business
plate: a clerk at a high desk among ledgers, 1880s
sections:
2.1 | What Accounting Is | new idea | 325
2.2 | Branches of Accounting | framework | 100
2.3 | Who Uses Accounting Information | framework | 425
2.4 | Principles, Standards and the Language of Business | framework | 550
concepts:
- 2.1 | Accounting as the language of business | standard | needs: none
- 2.1 | Recording, classifying, summarising and reporting | minor | needs: Accounting as the language of business
- 2.2 | Financial, management and cost accounting | minor | needs: none
- 2.3 | Internal users | standard | needs: none
- 2.3 | External users | minor | needs: Internal users
- 2.3 | What each user needs to know | minor | needs: External users
- 2.4 | Accounting concepts | standard | needs: none
- 2.4 | Accounting standards | standard | needs: Accounting concepts
- 2.4 | Why standards are necessary | minor | needs: Accounting standards
defines:
- Accounting | the process of recording, sorting, summarising and reporting the money events of a business
- Financial accounting | accounting that prepares reports on a business for people outside it, such as banks and tax officers
- Management accounting | accounting that gives a business's own managers the information they need to plan and decide
- Cost accounting | accounting that works out what it costs to make a product or provide a service
- User of accounting information | any person or group that reads accounting reports in order to make a decision
- Business entity concept | the rule that a business is kept separate from its owner when records are made
- Going concern concept | the assumption that a business will continue to operate for the foreseeable future
- Money measurement concept | the rule that only events that can be stated in money are recorded
- Historical cost concept | the rule that an asset is recorded at the price actually paid for it
- Accounting standard | a detailed rule, issued by an official body, on how a type of item must be recorded and reported
- Generally accepted accounting principles | the body of agreed rules that businesses follow when they prepare accounts
assumes: Business, Record, Owner, Customer, Supplier, Merchandising firm, Manufacturing firm, Service firm
words-in-use: standard
case: Meghna and Sons, illustrative. By 31 January 2022 the workshop owed Tk 20,000 to its machine supplier, Dhaka Machine Works. Four people wanted information about the workshop: Karim Meghna as owner; Dhaka Machine Works, which wanted to know whether the Tk 20,000 would be paid; a bank, to which Karim would apply for a loan in March 2022; and the National Board of Revenue, which collects income tax. No further figures are used.
history: The International Accounting Standards Committee was founded in 1973 by professional bodies from several countries and was replaced by the International Accounting Standards Board in 2001. Search: IASC founded 1973 IASB 2001.
refs: Chapter 1, 'Business, Money and Records', section 1.1 'Everyday Money and the Need for Records' — records are the raw material of accounting; Chapter 4, 'A First Look at the Financial Statements', section 4.1 'The Income Statement' — the reports that accounting produces
need: Chapter 1, 'Business, Money and Records', section 1.1 'Everyday Money and the Need for Records'
ladder: 1) a household using records to decide on a purchase; 2) one business and three different users; 3) the same facts reshaped for a new business, a pharmacy; 4) a case in which a standard, a concept and a user's need all apply.
practice: review: match a user with the information they need; say which concept a described practice follows; think: explain to a shop owner why the owner's home spending is kept out of the business records; pause: after 2.3
sources: no

=== CH03 ===
title: The Accounting Equation
purpose: Teach the five building blocks of the equation and how every transaction keeps it in balance.
pace: slow — the first idea in the book that the reader must hold and use
style: calculation
words: 4475
figures: 3
- fig01: the accounting equation as a balance scale
- fig02: how revenue, expenses and drawings flow into owner's equity
- fig03: a running equation table, one row per transaction
plate: a pair of brass balance scales on a counting-house desk beside a stack of coins, 1880s
sections:
3.1 | Assets, Liabilities and Owner's Equity | framework | 775
3.2 | Income, Expenses and Withdrawals | framework | 325
3.3 | Business Transactions | new idea | 325
3.4 | Summarising Transactions in the Equation | technique | 450
concepts:
- 3.1 | Assets and liabilities | standard | needs: none
- 3.1 | The equation: Assets = Liabilities + Owner's equity | core | needs: Assets and liabilities
- 3.2 | Revenue and expenses change equity | standard | needs: none
- 3.2 | Drawings | minor | needs: Revenue and expenses change equity
- 3.3 | What counts as a transaction | standard | needs: none
- 3.3 | Source documents | minor | needs: What counts as a transaction
- 3.4 | Analysing one transaction at a time | standard | needs: none
- 3.4 | Totalling the equation after each transaction | standard | needs: Analysing one transaction at a time
defines:
- Asset | something of value that a business owns or is owed, such as cash, equipment or money owed by customers
- Liability | an amount that a business owes to someone outside the business
- Owner's equity | the owner's claim on the business: what is left when liabilities are taken from assets
- Accounting equation | the statement that assets always equal liabilities plus owner's equity
- Revenue | the price of goods sold or services provided to customers in a period
- Expense | a cost of running the business that is used up in earning revenue
- Net income | the amount by which revenue is greater than expenses in a period
- Net loss | the amount by which expenses are greater than revenue in a period
- Drawings | money or goods the owner takes out of the business for personal use
- Transaction | an event that has a money value and changes the accounting equation
- Source document | a paper or electronic proof that a transaction took place, such as an invoice or receipt
- Account receivable | an amount a customer owes the business for goods or services already provided
- Account payable | an amount the business owes a supplier for goods or services already received
assumes: Business, Profit, Loss, Customer, Supplier, Owner, Record, Accounting
words-in-use: capital; equity; account
case: Meghna and Sons, illustrative. January 2022, transactions that change only cash, equipment, money owed and money earned: 2 Jan owner Karim Meghna invests cash Tk 600,000; 3 Jan buys binding equipment Tk 150,000, paying Tk 100,000 cash and owing Tk 50,000 to Dhaka Machine Works; 8 Jan binding work for cash Tk 95,000; 12 Jan binding work for a school on account Tk 120,000; 20 Jan collects Tk 70,000 from the school; 22 Jan pays Tk 30,000 to Dhaka Machine Works; 25 Jan pays wages Tk 40,000; 28 Jan pays utilities Tk 8,000; 31 Jan owner withdraws Tk 20,000. Running totals by code: cash Tk 567,000; accounts receivable Tk 50,000; equipment Tk 150,000; total assets Tk 767,000; accounts payable Tk 20,000; owner's equity Tk 747,000 (capital Tk 600,000 plus net income Tk 167,000 less drawings Tk 20,000). Revenue Tk 215,000; expenses Tk 48,000 (wages Tk 40,000, utilities Tk 8,000).
history: The Medici Bank of Florence, founded 1397 by Giovanni di Bicci de' Medici, kept ledgers that listed what the bank owned and owed. Search: Medici Bank ledgers balance 15th century.
refs: Chapter 4, 'A First Look at the Financial Statements', section 4.3 'The Balance Sheet' — the equation shown as a report; Chapter 5, 'Accounts, Debits and Credits', section 5.1 'The Account and Its Six Types' — the equation broken into six kinds of account
need: Chapter 1, 'Business, Money and Records', section 1.1 'Everyday Money and the Need for Records'; Chapter 2, 'Accounting, Its Users and Its Rules', section 2.1 'What Accounting Is'
ladder: 1) one owner puts in cash and the equation is checked; 2) a purchase on credit; 3) a full week of mixed events in round numbers; 4) a month of eight or more events with revenue, expenses and drawings.
practice: review: explain the equation in words; state the effect of a described event on assets, liabilities and equity; think: build the equation for a new small business after six events; pause: after 3.1 and after 3.3
sources: no

=== CH04 ===
title: A First Look at the Financial Statements
purpose: Show the three main reports in simple form, how they link, and how time is divided into periods.
pace: standard — the statements are previewed in simple form
style: mixed
words: 4025
figures: 2
- fig01: the three statements side by side with link arrows
- fig02: one month, one quarter and one year on a timeline
plate: a merchant reading a long roll of figures at a window above a harbour, 1880s
sections:
4.1 | The Income Statement | framework | 325
4.2 | The Statement of Owner's Equity | framework | 325
4.3 | The Balance Sheet | framework | 325
4.4 | How the Statements Connect; Accounting Periods | framework | 450
concepts:
- 4.1 | Revenue, expenses and net income laid out | standard | needs: none
- 4.1 | Reading the heading and the date | minor | needs: Revenue, expenses and net income laid out
- 4.2 | Opening capital, net income and drawings | standard | needs: none
- 4.2 | The closing capital figure | minor | needs: Opening capital, net income and drawings
- 4.3 | Assets on one side, claims on the other | standard | needs: none
- 4.3 | Listing order of items | minor | needs: Assets on one side, claims on the other
- 4.4 | The order of preparation and the links | standard | needs: none
- 4.4 | Fiscal year, calendar year and interim period | standard | needs: The order of preparation and the links
defines:
- Financial statement | a formal report that sums up the money results or position of a business
- Income statement | the report that shows revenue, expenses and the resulting net income or net loss for a period
- Statement of owner's equity | the report that shows how the owner's equity changed during a period
- Balance sheet | the report that lists the assets, liabilities and owner's equity of a business on one date
- Accounting period | the stretch of time, such as a month or a year, covered by one set of reports
- Fiscal year | a twelve-month accounting period that can start in any month, such as 1 July to 30 June
- Calendar year | the twelve months from 1 January to 31 December
- Interim period | a period shorter than a year, such as a month or quarter, for which reports are prepared
assumes: Asset, Liability, Owner's equity, Accounting equation, Revenue, Expense, Net income, Net loss, Drawings
words-in-use: balance; statement
case: Meghna and Sons, illustrative. Figures from the month ended 31 January 2022, with no adjustments yet. Revenue Tk 215,000 (binding work for cash Tk 95,000 and on account Tk 120,000). Expenses Tk 48,000 (wages Tk 40,000; utilities Tk 8,000). Net income Tk 167,000. Owner's equity: capital Tk 600,000 at 2 January, plus net income Tk 167,000, less drawings Tk 20,000, equals Tk 747,000. Assets at 31 January: cash Tk 567,000; accounts receivable Tk 50,000; equipment Tk 150,000; total Tk 767,000. Liabilities: accounts payable Tk 20,000.
history: The Dutch East India Company (VOC), founded 20 March 1602, was an early company whose investors pressed for reports on how their money was used. Search: VOC 1602 shareholders demand accounts.
refs: Chapter 3, 'The Accounting Equation', section 3.4 'Summarising Transactions in the Equation' — the equation these reports are built from; Chapter 10, 'Closing the Books', section 10.1 'Preparing the Statements from the Worksheet' — the same reports prepared from a worksheet
need: Chapter 3, 'The Accounting Equation', section 3.1 'Assets, Liabilities and Owner's Equity'; Chapter 3, 'The Accounting Equation', section 3.2 'Income, Expenses and Withdrawals'
ladder: 1) a one-line income statement for a lemonade stand; 2) the equity statement for the same stand; 3) a balance sheet for the workshop in round numbers; 4) all three for a new business, with a check that they agree.
practice: review: identify which statement holds a given item; check that a balance sheet balances; think: explain why the equity statement sits between the other two; pause: after 4.2
sources: no

=== CH05 ===
title: Accounts, Debits and Credits
purpose: Teach the six types of account, the rules of debit and credit, and double entry applied to transactions.
pace: slow — double entry is new, abstract and the base for every later chapter
style: calculation
words: 4450
figures: 3
- fig01: a T-account with its debit and credit sides labelled
- fig02: a table of the six account types with their increase side
- fig03: one transaction analysed in four steps
plate: two clerks facing each other across a desk, one reading aloud from a paper and one writing, 1880s
sections:
5.1 | The Account and Its Six Types | new idea | 325
5.2 | Debit and Credit | new idea | 650
5.3 | Double Entry in Practice | defining theory | 775
5.4 | T-Accounts | technique | 100
concepts:
- 5.1 | What an account is | standard | needs: none
- 5.1 | Six types of account and the chart of accounts | minor | needs: What an account is
- 5.2 | Debit on the left, credit on the right: the rules for each type | core | needs: none
- 5.2 | Normal balance | minor | needs: Debit on the left, credit on the right: the rules for each type
- 5.3 | Every transaction has two sides | core | needs: none
- 5.3 | Analysing a transaction in four steps | standard | needs: Every transaction has two sides
- 5.4 | Drawing and balancing a T-account | minor | needs: none
defines:
- Account | a record of the increases and decreases in one kind of item, such as Cash or Wages Expense
- Chart of accounts | the numbered list of all the accounts a business uses
- Debit | an entry on the left side of an account
- Credit | an entry on the right side of an account
- Normal balance | the side of an account, debit or credit, on which its increases are recorded
- Double-entry system | the method in which every transaction is recorded as equal debits and credits in at least two accounts
- T-account | a simple drawing of an account, shaped like the letter T, with debits on the left and credits on the right
- Account balance | the difference between the total debits and the total credits in an account
assumes: Asset, Liability, Owner's equity, Revenue, Expense, Drawings, Transaction, Source document, Account receivable, Account payable, Accounting equation
words-in-use: account; debit; credit
case: Meghna and Sons, illustrative. January 2022 transactions: 2 Jan owner Karim Meghna invests cash Tk 600,000; 3 Jan buys binding equipment Tk 150,000, paying Tk 100,000 cash and owing Tk 50,000 to Dhaka Machine Works; 8 Jan binding work for cash Tk 95,000; 12 Jan binding work for a school on account Tk 120,000; 20 Jan collects Tk 70,000 from the school; 22 Jan pays Tk 30,000 to Dhaka Machine Works; 25 Jan pays wages Tk 40,000; 28 Jan pays utilities Tk 8,000; 31 Jan owner withdraws Tk 20,000. Six account types used: assets (Cash, Accounts Receivable, Equipment); liabilities (Accounts Payable); owner's equity (Owner's Capital); drawings (Owner's Drawings); revenue (Service Revenue); expenses (Wages Expense, Utilities Expense). Account balances by code at 31 January: Cash Tk 567,000 debit; Accounts Receivable Tk 50,000 debit; Equipment Tk 150,000 debit; Accounts Payable Tk 20,000 credit; Owner's Capital Tk 600,000 credit; Owner's Drawings Tk 20,000 debit; Service Revenue Tk 215,000 credit; Wages Expense Tk 40,000 debit; Utilities Expense Tk 8,000 debit.
history: Luca Pacioli's Summa de arithmetica, printed in Venice in 1494, contained a treatise that described double-entry bookkeeping as used by Venetian merchants. Search: Pacioli Summa 1494 double entry treatise.
refs: Chapter 3, 'The Accounting Equation', section 3.1 'Assets, Liabilities and Owner's Equity' — the equation that double entry protects; Chapter 6, 'Journal and Ledger', section 6.1 'The Journal and Journal Entries' — where debits and credits are first written down
need: Chapter 3, 'The Accounting Equation', section 3.1 'Assets, Liabilities and Owner's Equity'; Chapter 3, 'The Accounting Equation', section 3.3 'Business Transactions'
ladder: 1) one cash investment shown in two accounts; 2) a purchase part cash, part on credit; 3) a month of nine transactions analysed in T-accounts with small round numbers; 4) a mixed case with revenue, an expense, drawings and a payment on credit.
practice: review: state which accounts increase with a debit and which with a credit; analyse new transactions in four steps; think: explain to a beginner why a debit can be good news for one account and bad news for another; pause: after 5.1, 5.2 and 5.3
sources: yes

=== CH06 ===
title: Journal and Ledger
purpose: Show how transactions are first recorded in the journal and then posted to the ledger.
pace: standard — it organises what chapter 5 already taught
style: calculation
words: 4225
figures: 2
- fig01: a journal page with columns labelled
- fig02: an arrow from journal entry to the ledger accounts it feeds
plate: a long shelf of leather-bound ledgers with a wheeled library ladder, 1880s
sections:
6.1 | The Journal and Journal Entries | technique | 650
6.2 | The Ledger and Posting | technique | 650
6.3 | Worked Cycle of Entries | technique | 325
concepts:
- 6.1 | Layout of a journal entry | core | needs: none
- 6.1 | Narration and compound entries | minor | needs: Layout of a journal entry
- 6.2 | The ledger as the book of accounts | core | needs: none
- 6.2 | Posting step by step and cross-referencing | minor | needs: The ledger as the book of accounts
- 6.3 | A month from journal to ledger balances | standard | needs: none
- 6.3 | Checking your own work | minor | needs: A month from journal to ledger balances
defines:
- Journal | the book in which each transaction is first recorded, in date order
- Journal entry | one recorded transaction, showing the accounts debited and credited and the amounts
- Compound entry | a journal entry that affects more than two accounts
- Narration | a short written explanation placed under a journal entry
- Ledger | the complete set of accounts of a business, kept together
- Posting | copying the amounts from journal entries into the proper ledger accounts
- Folio | a page or reference number used to link a journal entry with its ledger account
assumes: Account, Debit, Credit, Double-entry system, T-account, Account balance, Transaction, Source document
words-in-use: book; entry
case: Meghna and Sons, illustrative. January 2022 transactions: 2 Jan owner Karim Meghna invests cash Tk 600,000; 3 Jan buys binding equipment Tk 150,000, paying Tk 100,000 cash and owing Tk 50,000 to Dhaka Machine Works; 8 Jan binding work for cash Tk 95,000; 12 Jan binding work for a school on account Tk 120,000; 20 Jan collects Tk 70,000 from the school; 22 Jan pays Tk 30,000 to Dhaka Machine Works; 25 Jan pays wages Tk 40,000; 28 Jan pays utilities Tk 8,000; 31 Jan owner withdraws Tk 20,000. Ledger balances after posting (by code): Cash Tk 567,000 Dr; Accounts Receivable Tk 50,000 Dr; Equipment Tk 150,000 Dr; Accounts Payable Tk 20,000 Cr; Owner's Capital Tk 600,000 Cr; Owner's Drawings Tk 20,000 Dr; Service Revenue Tk 215,000 Cr; Wages Expense Tk 40,000 Dr; Utilities Expense Tk 8,000 Dr. Equipment purchase of 3 January is the compound entry: Equipment Dr Tk 150,000; Cash Cr Tk 100,000; Accounts Payable Cr Tk 50,000.
history: The ledger of Giovanni Farolfi and Company, kept 1299 to 1300 at Salon-de-Provence, is one of the oldest known surviving double-entry ledgers. Search: Farolfi ledger 1299 double entry earliest.
refs: Chapter 5, 'Accounts, Debits and Credits', section 5.3 'Double Entry in Practice' — the entries are journalised from this analysis; Chapter 7, 'The Trial Balance and the Accounting Cycle', section 7.1 'Preparing a Trial Balance' — the ledger balances are listed in a trial balance
need: Chapter 5, 'Accounts, Debits and Credits', section 5.2 'Debit and Credit'; Chapter 5, 'Accounts, Debits and Credits', section 5.3 'Double Entry in Practice'
ladder: 1) one entry written in journal form; 2) a compound entry; 3) the first week of the workshop journalised and posted; 4) a full month, with ledger balances checked.
practice: review: write the entry for a described event; post a given entry to T-accounts; think: find which of three journal entries is written wrongly and say why; pause: after 6.1 and 6.2
sources: no

=== CH07 ===
title: The Trial Balance and the Accounting Cycle
purpose: Teach how to test the ledger with a trial balance, handle errors, and see the steps of the accounting cycle.
pace: standard — a checking tool and an overview
style: mixed
words: 3900
figures: 2
- fig01: a trial balance with the two total lines highlighted
- fig02: the accounting cycle as a circle of steps
plate: a clerk with a magnifying glass over a long column of figures beside an inkwell, 1880s
sections:
7.1 | Preparing a Trial Balance | technique | 650
7.2 | Finding and Correcting Errors | technique | 325
7.3 | Steps of the Accounting Cycle | framework | 325
concepts:
- 7.1 | Listing ledger balances in two columns | core | needs: none
- 7.1 | What equal totals do and do not prove | minor | needs: Listing ledger balances in two columns
- 7.2 | Errors that stop the totals agreeing | standard | needs: none
- 7.2 | Errors the trial balance cannot find | minor | needs: Errors that stop the totals agreeing
- 7.3 | The cycle from transaction to closing | standard | needs: none
- 7.3 | Where each later chapter fits | minor | needs: The cycle from transaction to closing
defines:
- Trial balance | a list of all ledger account balances showing that total debits equal total credits
- Transposition error | a mistake in which two digits of a number are written in the wrong order
- Error of omission | a mistake in which a transaction, or one side of it, is left out of the records
- Compensating error | two mistakes of equal size on opposite sides that cancel each other out
- Accounting cycle | the full set of steps from recording a transaction to preparing the next period's opening records
assumes: Ledger, Posting, Journal, Account balance, Debit, Credit, Financial statement, Accounting period
words-in-use: balance; trial
case: Meghna and Sons, illustrative. Ledger balances at 31 January 2022: Cash Tk 567,000 Dr; Accounts Receivable Tk 50,000 Dr; Equipment Tk 150,000 Dr; Owner's Drawings Tk 20,000 Dr; Wages Expense Tk 40,000 Dr; Utilities Expense Tk 8,000 Dr; Accounts Payable Tk 20,000 Cr; Owner's Capital Tk 600,000 Cr; Service Revenue Tk 215,000 Cr. Debit total Tk 835,000; credit total Tk 835,000. Three faulty copies: (a) Equipment copied as Tk 105,000, so debits are Tk 790,000, a difference of Tk 45,000; (b) the credit to Accounts Receivable for the 20 January collection of Tk 70,000 was never posted, so Accounts Receivable shows Tk 120,000 and debits total Tk 905,000 against credits of Tk 835,000; (c) Wages Expense copied as Tk 45,000 and Owner's Drawings copied as Tk 15,000, so the totals still agree at Tk 835,000.
history: Barings Bank collapsed in February 1995 after trading losses were hidden in an error account numbered 88888 in its Singapore office. Search: Barings 1995 account 88888 Leeson.
refs: Chapter 6, 'Journal and Ledger', section 6.2 'The Ledger and Posting' — the ledger balances the trial balance lists; Chapter 8, 'Adjusting the Accounts', section 8.1 'Why Accounts Need Adjusting' — the next step in the cycle; Chapter 9, 'The Worksheet', section 9.1 'What a Worksheet Is and Why It Helps' — a worksheet that includes the trial balance
need: Chapter 6, 'Journal and Ledger', section 6.1 'The Journal and Journal Entries'; Chapter 6, 'Journal and Ledger', section 6.2 'The Ledger and Posting'
ladder: 1) a six-account trial balance in round numbers; 2) one transposition error found by dividing by nine; 3) a trial balance with a missing balance and a wrong side; 4) a complete trial balance for the workshop with a hidden compensating error.
practice: review: prepare a trial balance from given balances; say which errors the totals will reveal; think: explain why equal totals do not prove the books are right; pause: after 7.1
sources: no

=== CH08 ===
title: Adjusting the Accounts
purpose: Teach why period-end adjustments are needed and how to record each type, ending with the adjusted trial balance.
pace: slow — accruals and deferrals are new, abstract and have many moving parts
style: calculation
words: 5575
figures: 3
- fig01: a timeline showing a payment made before, and a cost used after, the month-end
- fig02: the four adjustment types in a two-by-two grid
- fig03: before-and-after trial balance columns for one adjustment
plate: a grandfather clock beside a stack of unpaid bills and receipts on a merchant's desk, 1880s
sections:
8.1 | Why Accounts Need Adjusting | new idea | 775
8.2 | Prepaid Items and Unearned Revenue | technique | 775
8.3 | Accrued Items | technique | 775
8.4 | Depreciation as an Adjustment | technique | 325
8.5 | The Adjusted Trial Balance | technique | 325
concepts:
- 8.1 | Cash basis and accrual basis | standard | needs: none
- 8.1 | The matching principle and adjusting entries | core | needs: Cash basis and accrual basis
- 8.2 | Prepaid expenses and supplies used | core | needs: none
- 8.2 | Unearned revenue earned over time | standard | needs: Prepaid expenses and supplies used
- 8.3 | Accrued expenses such as unpaid wages | core | needs: none
- 8.3 | Accrued revenue not yet billed | standard | needs: Accrued expenses such as unpaid wages
- 8.4 | Spreading the cost of equipment over its life | standard | needs: none
- 8.4 | Accumulated depreciation as a contra account | minor | needs: Spreading the cost of equipment over its life
- 8.5 | Applying the six adjustments to the trial balance | standard | needs: none
- 8.5 | Checking that totals still agree | minor | needs: Applying the six adjustments to the trial balance
defines:
- Adjusting entry | a journal entry made at the end of a period to bring an account up to its correct amount
- Cash basis | the method of recording revenue and expenses only when cash is received or paid
- Accrual basis | the method of recording revenue when it is earned and expenses when they are incurred, whatever the cash timing
- Matching principle | the rule that expenses are recorded in the same period as the revenue they helped to earn
- Prepaid expense | a cost paid in advance, held as an asset until its benefit is used up
- Unearned revenue | money received before the work is done, held as a liability until the work is performed
- Accrued expense | a cost already incurred in the period but not yet paid or recorded
- Accrued revenue | revenue earned in the period but not yet received or billed
- Depreciation | the sharing of an asset's cost across the periods in which the asset is used
- Accumulated depreciation | the total depreciation charged on an asset since it was bought
- Contra account | an account that is deducted from a related account and has the opposite normal balance
- Adjusted trial balance | a trial balance prepared after the adjusting entries have been posted
assumes: Trial balance, Journal entry, Ledger, Posting, Asset, Liability, Revenue, Expense, Accounting cycle, Accounting period
words-in-use: charge; supplies; accrual
case: Meghna and Sons, illustrative. Unadjusted trial balance at 31 January 2022 (Dr): Cash Tk 555,000; Accounts Receivable Tk 50,000; Supplies Tk 18,000; Prepaid Rent Tk 36,000; Equipment Tk 150,000; Owner's Drawings Tk 20,000; Wages Expense Tk 40,000; Utilities Expense Tk 8,000. (Cr): Accounts Payable Tk 38,000; Unearned Revenue Tk 24,000; Owner's Capital Tk 600,000; Service Revenue Tk 215,000. Each total Tk 877,000. Three events since the chapter 5 list: 2 Jan three months' rent paid in advance, Tk 36,000; 4 Jan supplies bought on account, Tk 18,000; 2 Jan a library paid Tk 24,000 for a 12-month repair contract running from 1 January. Month-end facts: (a) one month of rent used, Tk 12,000; (b) supplies on hand Tk 7,000, so Tk 11,000 used; (c) equipment cost Tk 150,000, residual Tk 30,000, 10 years, depreciation for one month Tk 1,000; (d) wages for the last days of January, unpaid, Tk 9,000; (e) one month of the library contract earned, Tk 2,000; (f) binding work finished but not billed, Tk 15,000. Adjusted balances by code: Accounts Receivable Tk 65,000; Supplies Tk 7,000; Prepaid Rent Tk 24,000; Accumulated Depreciation Tk 1,000 Cr; Wages Payable Tk 9,000 Cr; Unearned Revenue Tk 22,000 Cr; Service Revenue Tk 232,000 Cr; Wages Expense Tk 49,000; Rent Expense Tk 12,000; Supplies Expense Tk 11,000; Depreciation Expense Tk 1,000. Adjusted totals Tk 902,000 each side.
history: In September 2014 the British supermarket group Tesco announced that its profit had been overstated, because income from suppliers had been recorded too early. Search: Tesco 2014 profit overstatement supplier income timing.
refs: Chapter 7, 'The Trial Balance and the Accounting Cycle', section 7.3 'Steps of the Accounting Cycle' — adjusting is the next step in the cycle; Chapter 9, 'The Worksheet', section 9.1 'What a Worksheet Is and Why It Helps' — the worksheet carries these adjustments; Chapter 15, 'Plant Assets and Depreciation', section 15.2 'Why We Depreciate; Factors That Affect It' — depreciation taught fully later
need: Chapter 7, 'The Trial Balance and the Accounting Cycle', section 7.1 'Preparing a Trial Balance'; Chapter 7, 'The Trial Balance and the Accounting Cycle', section 7.3 'Steps of the Accounting Cycle'
ladder: 1) one month's insurance paid in advance; 2) the same idea for supplies and for money received in advance; 3) accrued wages and accrued revenue, one at a time; 4) a month-end with all six adjustments and a new trial balance.
practice: review: write the adjusting entry for a described situation; say which accounts it changes; think: explain how an unadjusted profit figure could mislead a lender; pause: after 8.1, 8.2 and 8.3
sources: no

=== CH09 ===
title: The Worksheet
purpose: Show how a ten-column worksheet joins the trial balance, adjustments and statement figures on one page.
pace: slow — ten columns carry many ideas at once
style: calculation
words: 4475
figures: 2
- fig01: the ten columns as a labelled grid
- fig02: arrows showing which accounts move to which statement column
plate: a drawing board with a wide ruled sheet, set squares and compasses, 1880s
sections:
9.1 | What a Worksheet Is and Why It Helps | framework | 325
9.2 | Building the Ten-Column Worksheet | technique | 1100
9.3 | A Service Company Worked Through | technique | 450
concepts:
- 9.1 | The worksheet as a working paper | standard | needs: none
- 9.1 | When and by whom it is prepared | minor | needs: The worksheet as a working paper
- 9.2 | Trial balance and adjustment columns | core | needs: none
- 9.2 | Adjusted trial balance, statement and balance sheet columns | core | needs: Trial balance and adjustment columns
- 9.3 | Filling every column for the workshop | standard | needs: none
- 9.3 | Finding net income as the balancing figure | standard | needs: Filling every column for the workshop
defines:
- Worksheet | a working paper, not a formal report, that lays out the trial balance, adjustments and statement figures in columns
- Ten-column worksheet | a worksheet with five pairs of debit and credit columns, from unadjusted trial balance to balance sheet
- Footing | adding up a column of figures to get its total
assumes: Trial balance, Adjusting entry, Adjusted trial balance, Income statement, Balance sheet, Net income, Net loss
words-in-use: working
case: Meghna and Sons, illustrative. Trial balance at 31 January 2022 (Dr): Cash Tk 555,000; Accounts Receivable Tk 50,000; Supplies Tk 18,000; Prepaid Rent Tk 36,000; Equipment Tk 150,000; Owner's Drawings Tk 20,000; Wages Expense Tk 40,000; Utilities Expense Tk 8,000 (total Tk 877,000). (Cr): Accounts Payable Tk 38,000; Unearned Revenue Tk 24,000; Owner's Capital Tk 600,000; Service Revenue Tk 215,000 (total Tk 877,000). Adjustments: (a) Rent Expense Dr, Prepaid Rent Cr Tk 12,000; (b) Supplies Expense Dr, Supplies Cr Tk 11,000; (c) Depreciation Expense Dr, Accumulated Depreciation Cr Tk 1,000; (d) Wages Expense Dr, Wages Payable Cr Tk 9,000; (e) Unearned Revenue Dr, Service Revenue Cr Tk 2,000; (f) Accounts Receivable Dr, Service Revenue Cr Tk 15,000. Adjusted totals Tk 902,000 each side. Income statement columns: debits (expenses) Tk 81,000, credits (revenue) Tk 232,000, net income Tk 151,000. Balance sheet columns: debits Tk 821,000, credits Tk 670,000, difference Tk 151,000.
history: VisiCalc, the first spreadsheet program for personal computers, was released in 1979 for the Apple II by Dan Bricklin and Bob Frankston. Search: VisiCalc 1979 Bricklin Frankston paper ledger.
refs: Chapter 8, 'Adjusting the Accounts', section 8.5 'The Adjusted Trial Balance' — the adjusted trial balance feeds the worksheet; Chapter 10, 'Closing the Books', section 10.1 'Preparing the Statements from the Worksheet' — statements are prepared from the finished worksheet
need: Chapter 7, 'The Trial Balance and the Accounting Cycle', section 7.1 'Preparing a Trial Balance'; Chapter 8, 'Adjusting the Accounts', section 8.5 'The Adjusted Trial Balance'
ladder: 1) a worksheet with three accounts and one adjustment; 2) five accounts and two adjustments; 3) the workshop's twelve accounts and six adjustments; 4) a worksheet for a new service business with a net loss.
practice: review: say what each column pair does; complete a partly filled worksheet; think: explain why a worksheet is optional and why accountants still use it; pause: after 9.2
sources: no

=== CH10 ===
title: Closing the Books
purpose: Show how statements are drawn from the worksheet and how temporary accounts are closed for the next period.
pace: standard — it applies the worksheet
style: calculation
words: 4025
figures: 2
- fig01: the four closing entries as arrows into the income summary and capital accounts
- fig02: before-and-after view of temporary and permanent accounts
plate: a clerk locking a heavy iron safe at evening by candlelight, 1880s
sections:
10.1 | Preparing the Statements from the Worksheet | technique | 325
10.2 | Closing Entries | technique | 775
10.3 | Reversing Entries | technique | 325
concepts:
- 10.1 | Income statement and equity statement from the worksheet | standard | needs: none
- 10.1 | Balance sheet from the worksheet | minor | needs: Income statement and equity statement from the worksheet
- 10.2 | Why temporary accounts are closed | core | needs: none
- 10.2 | The four closing entries | standard | needs: Why temporary accounts are closed
- 10.3 | What a reversing entry undoes | standard | needs: none
- 10.3 | When reversing is optional | minor | needs: What a reversing entry undoes
defines:
- Closing entry | a journal entry at the end of a period that moves a temporary account's balance to equity
- Temporary account | an account for revenue, expense or drawings that is closed to zero at the end of each period
- Permanent account | an account for an asset, liability or owner's capital whose balance carries into the next period
- Income summary | a temporary account that collects revenue and expenses before the net result moves to capital
- Reversing entry | an entry made on the first day of a new period that cancels an earlier adjusting entry
assumes: Worksheet, Adjusting entry, Accrued expense, Accrued revenue, Financial statement, Income statement, Statement of owner's equity, Balance sheet, Fiscal year
words-in-use: close; summary
case: Meghna and Sons, illustrative. Adjusted balances at 31 January 2022, from the worksheet: Cash Tk 555,000; Accounts Receivable Tk 65,000; Supplies Tk 7,000; Prepaid Rent Tk 24,000; Equipment Tk 150,000; Accumulated Depreciation Tk 1,000 Cr; Accounts Payable Tk 38,000; Wages Payable Tk 9,000; Unearned Revenue Tk 22,000; Owner's Capital Tk 600,000; Owner's Drawings Tk 20,000; Service Revenue Tk 232,000; Wages Expense Tk 49,000; Utilities Expense Tk 8,000; Rent Expense Tk 12,000; Supplies Expense Tk 11,000; Depreciation Expense Tk 1,000. Net income Tk 151,000 (revenue Tk 232,000 less expenses Tk 81,000). Closing capital Tk 731,000 (Tk 600,000 plus Tk 151,000 less Tk 20,000). Total assets Tk 800,000; total liabilities Tk 69,000. Reversing entry for the Tk 9,000 wages accrual is made on 1 February 2022.
history: The British tax year begins on 6 April because of the calendar change of 1752, when eleven days were dropped and the old year-end of 25 March was moved forward. Search: why UK tax year starts 6 April 1752 calendar.
refs: Chapter 9, 'The Worksheet', section 9.3 'A Service Company Worked Through' — the worksheet this chapter draws from; Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.3 'The Classified Income Statement' — statements for a trading firm with classified headings
need: Chapter 9, 'The Worksheet', section 9.2 'Building the Ten-Column Worksheet'; Chapter 9, 'The Worksheet', section 9.3 'A Service Company Worked Through'
ladder: 1) close one revenue account; 2) close revenue, expenses and drawings for a tiny firm; 3) the workshop's closing entries from the worksheet; 4) a full set of statements and closing entries for a new service business.
practice: review: write closing entries from a list of balances; say which accounts stay open; think: explain why drawings are not closed to the income summary; pause: after 10.2
sources: no

=== CH11 ===
title: Merchandising Company Accounts and Classified Statements
purpose: Show how buying and selling goods changes the accounts and how classified statements group items.
pace: standard — the new items are small and attach to what is known
style: mixed
words: 4650
figures: 3
- fig01: goods flowing from supplier to shop to customer with the account for each step
- fig02: a classified income statement with section brackets
- fig03: a classified balance sheet with current and non-current groups
plate: a busy shop counter with shelves of books, string and paper parcels, 1880s
sections:
11.1 | Buying and Selling Goods | new idea | 650
11.2 | Product Costs and Period Costs | framework | 100
11.3 | The Classified Income Statement | framework | 650
11.4 | The Classified Balance Sheet | framework | 650
concepts:
- 11.1 | Purchases, sales, returns and freight | core | needs: none
- 11.1 | Cost of goods sold and gross profit | minor | needs: Purchases, sales, returns and freight
- 11.2 | Product costs versus period costs | minor | needs: none
- 11.3 | Net sales, cost of goods sold and gross profit | core | needs: none
- 11.3 | Operating expenses and net income | minor | needs: Net sales, cost of goods sold and gross profit
- 11.4 | Current and non-current assets and liabilities | core | needs: none
- 11.4 | Why the grouping helps a lender | minor | needs: Current and non-current assets and liabilities
defines:
- Merchandise inventory | the goods a merchandising firm holds for resale
- Purchases | the cost of goods bought during the period for resale
- Sales | the selling price of goods sold to customers during the period
- Sales return | goods that a customer sends back, reducing sales
- Purchase return | goods that the firm sends back to a supplier, reducing purchases
- Freight-in | the cost of carrying purchased goods to the firm's premises
- Cost of goods sold | the cost of the goods that were sold during the period
- Gross profit | net sales less cost of goods sold
- Product cost | a cost included in the cost of the goods themselves
- Period cost | a cost of running the business that is charged to the period in which it occurs
- Operating expense | a cost of running the business apart from the cost of goods sold
- Classified income statement | an income statement that groups items into sections such as sales, cost of goods sold and operating expenses
- Current asset | an asset expected to be turned into cash or used within one year
- Non-current asset | an asset the firm expects to use for longer than one year
- Current liability | a debt due for payment within one year
- Non-current liability | a debt not due for payment until after one year
- Classified balance sheet | a balance sheet that groups assets and liabilities into current and non-current sections
assumes: Income statement, Balance sheet, Revenue, Expense, Asset, Liability, Net income, Merchandising firm, Closing entry, Fiscal year
words-in-use: cost; goods; current
case: Meghna and Sons, illustrative. Year ended 31 December 2024, book sales. Sales Tk 3,100,000; sales returns Tk 40,000; inventory at 1 January Tk 180,000; purchases Tk 1,900,000; freight-in Tk 30,000; purchase returns Tk 25,000; inventory at 31 December Tk 210,000. Selling expenses: wages Tk 420,000; advertising Tk 60,000; delivery Tk 36,000. Administrative expenses: rent Tk 144,000; utilities Tk 48,000; insurance Tk 36,000; supplies Tk 24,000; depreciation Tk 45,000. Interest expense Tk 36,000. By code: net sales Tk 3,060,000; goods available Tk 2,085,000; cost of goods sold Tk 1,875,000; gross profit Tk 1,185,000; operating expenses Tk 813,000; operating profit Tk 372,000; net income Tk 336,000. Balance sheet at 31 December 2024: cash Tk 330,000; accounts receivable Tk 140,000; merchandise inventory Tk 210,000; supplies Tk 12,000; prepaid insurance Tk 18,000; equipment Tk 450,000 less accumulated depreciation Tk 90,000. Accounts payable Tk 160,000; wages payable Tk 14,000; unearned revenue Tk 10,000; bank loan Tk 300,000 repayable in three yearly instalments of Tk 100,000 from 2025 to 2027, so Tk 100,000 is current and Tk 200,000 is non-current. Total assets Tk 1,070,000; owner's capital at 1 January Tk 370,000; drawings Tk 120,000; closing capital Tk 586,000.
history: Amazon began selling books online from Seattle in July 1995, an example of a merchandising firm built on buying and reselling goods. Search: Amazon 1995 first books sold online.
refs: Chapter 10, 'Closing the Books', section 10.1 'Preparing the Statements from the Worksheet' — statements with simple headings; Chapter 12, 'Special Journals and the Cash Book', section 12.1 'Why Special Journals Exist' — special journals for repeated buying and selling; Chapter 14, 'Inventory', section 14.1 'What Inventory Is and Its Types' — inventory studied in depth
need: Chapter 4, 'A First Look at the Financial Statements', section 4.1 'The Income Statement'; Chapter 4, 'A First Look at the Financial Statements', section 4.3 'The Balance Sheet'; Chapter 10, 'Closing the Books', section 10.2 'Closing Entries'
ladder: 1) one purchase and one sale in round numbers; 2) cost of goods sold for a small shop; 3) a classified income statement for a month; 4) both classified statements for a full year with a loan.
practice: review: compute net sales, cost of goods sold and gross profit; classify given items as current or non-current; think: explain why a lender looks at the current groups first; pause: after 11.1
sources: no

=== CH12 ===
title: Special Journals and the Cash Book
purpose: Show how repeated transactions are grouped in special journals and how the cash book records receipts and payments.
pace: standard — a time-saving method built on the general journal
style: calculation
words: 4475
figures: 2
- fig01: a purchases journal and a sales journal with their columns
- fig02: a cash book with a receipts side and a payments side
plate: a post-office sorting table with pigeonholes and tied bundles of letters, 1880s
sections:
12.1 | Why Special Journals Exist | new idea | 325
12.2 | Purchases and Sales Journals | technique | 775
12.3 | The Cash Book and Cash Disbursements | technique | 775
concepts:
- 12.1 | Repeated transactions and the time they waste | standard | needs: none
- 12.1 | The general journal still has a place | minor | needs: Repeated transactions and the time they waste
- 12.2 | Recording purchases on credit | core | needs: none
- 12.2 | Recording sales on credit | standard | needs: Recording purchases on credit
- 12.3 | Cash receipts and the cash book | core | needs: none
- 12.3 | Cash disbursements journal | standard | needs: Cash receipts and the cash book
defines:
- Special journal | a journal used for only one kind of repeated transaction, such as credit purchases
- General journal | the journal used for transactions that no special journal covers
- Invoice | a document sent by a seller stating the goods or services supplied and the amount due
- Purchases journal | the special journal for goods bought on credit
- Sales journal | the special journal for goods sold on credit
- Cash receipts journal | the special journal for all money received
- Cash disbursements journal | the special journal for all money paid out
- Cash book | a book that records the receipts and payments passing through the firm's bank account
assumes: Journal, Journal entry, Ledger, Posting, Account receivable, Account payable, Purchases, Sales, Merchandise inventory, Invoice
words-in-use: book; cash
case: Meghna and Sons, illustrative. May 2024. Credit purchases: 3 May Padma Books Ltd Tk 120,000; 11 May Jamuna Distributors Tk 85,000; 19 May Padma Books Ltd Tk 60,000; 27 May Surma Stationers Tk 45,000 (total Tk 310,000). Credit sales: 4 May Dhaka Public School Tk 70,000; 13 May Green Valley College Tk 95,000; 22 May Notun Library Tk 40,000 (total Tk 205,000). Bank receipts: 9 May cash sales banked Tk 150,000; 20 May Dhaka Public School Tk 70,000; 28 May Green Valley College Tk 95,000 (total Tk 315,000). Bank payments: 15 May Padma Books Ltd, cheque 5001 Tk 120,000; 17 May rent, cheque 5002 Tk 12,000; 25 May wages, cheque 5003 Tk 35,000; 30 May Jamuna Distributors, cheque 5004 Tk 85,000 (total Tk 252,000). Bank balance at 1 May Tk 250,000; cash book balance at 31 May Tk 313,000. Unpaid at 31 May: Padma Books Ltd Tk 60,000 and Surma Stationers Tk 45,000; Notun Library owes Tk 40,000.
history: Francesco di Marco Datini, a merchant of Prato (about 1335 to 1410), kept many separate books for his trade; the surviving archive holds hundreds of ledgers and tens of thousands of letters. Search: Datini archive Prato ledgers letters.
refs: Chapter 6, 'Journal and Ledger', section 6.1 'The Journal and Journal Entries' — the general journal these journals relieve; Chapter 13, 'Bank Reconciliation', section 13.1 'Cash Book and Bank Statement' — the cash book is compared with the bank statement; Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.1 'Buying and Selling Goods' — the purchases and sales accounts these journals feed
need: Chapter 6, 'Journal and Ledger', section 6.1 'The Journal and Journal Entries'; Chapter 6, 'Journal and Ledger', section 6.2 'The Ledger and Posting'; Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.1 'Buying and Selling Goods'
ladder: 1) three credit purchases in a purchases journal; 2) a sales journal with a total posted; 3) a month of cash receipts and payments in a cash book; 4) a full month using all special journals and the general journal.
practice: review: say which journal a described transaction belongs in; total a special journal and name the accounts the total is posted to; think: explain why a shop with ten sales a day would not use only the general journal; pause: after 12.2
sources: no

=== CH13 ===
title: Bank Reconciliation
purpose: Teach how to compare the cash book with the bank statement and explain every difference.
pace: standard — one comparison, done carefully
style: calculation
words: 4350
figures: 2
- fig01: a cash book and a bank statement side by side with matching items marked
- fig02: the reconciliation statement as a two-column layout
plate: a bank teller behind a brass-grilled window counting coins into a tray, 1880s
sections:
13.1 | Cash Book and Bank Statement | framework | 325
13.2 | Causes of Differences; Debit and Credit Memos | framework | 650
13.3 | Preparing the Reconciliation Statement | technique | 775
concepts:
- 13.1 | Two records of one bank account | standard | needs: none
- 13.1 | Why the balances rarely agree | minor | needs: Two records of one bank account
- 13.2 | Timing differences: deposits in transit and outstanding cheques | core | needs: none
- 13.2 | Items the bank records first: charges and direct deposits | minor | needs: Timing differences: deposits in transit and outstanding cheques
- 13.3 | The two-sided reconciliation layout | core | needs: none
- 13.3 | Journal entries after reconciling | standard | needs: The two-sided reconciliation layout
defines:
- Bank statement | a report from the bank listing the deposits, withdrawals and balance on the firm's account
- Bank reconciliation statement | a statement that explains the difference between the cash book balance and the bank statement balance
- Outstanding cheque | a cheque the firm has written and recorded but the bank has not yet paid
- Deposit in transit | money the firm has recorded as banked but the bank has not yet added to its statement
- Debit memo | a bank notice that it has taken money out of the firm's account, for example a charge
- Credit memo | a bank notice that it has added money to the firm's account, for example a direct customer payment
- Adjusted cash balance | the correct bank balance after all reconciling items have been included
assumes: Cash book, Ledger, Journal entry, Account balance, Debit, Credit, Cash receipts journal, Cash disbursements journal
words-in-use: statement; balance; deposit
case: Meghna and Sons, illustrative. Cash book balance at 31 May 2024 Tk 313,000 (see May 2024 receipts and payments). Items found when the bank statement arrived: cheque 5004 for Tk 85,000 to Jamuna Distributors not yet presented; the Tk 95,000 received from Green Valley College on 28 May banked on 31 May but not yet shown by the bank; bank charges of Tk 1,500 not yet in the cash book; a direct payment of Tk 8,000 from Notun Library into the bank, not yet in the cash book. By code: adjusted cash book balance Tk 319,500; bank statement balance Tk 309,500.
history: In February 2016 criminals sent fraudulent payment instructions in the name of Bangladesh Bank, and about US$81 million reached accounts in the Philippines. Search: Bangladesh Bank 2016 SWIFT heist US$81 million.
refs: Chapter 12, 'Special Journals and the Cash Book', section 12.3 'The Cash Book and Cash Disbursements' — the cash book being checked; Chapter 8, 'Adjusting the Accounts', section 8.1 'Why Accounts Need Adjusting' — the idea that records must be brought up to date
need: Chapter 12, 'Special Journals and the Cash Book', section 12.3 'The Cash Book and Cash Disbursements'
ladder: 1) one outstanding cheque; 2) one deposit in transit plus one bank charge; 3) the four items for May in a full statement; 4) a reconciliation with an error in the cash book.
practice: review: say which side each item is added or subtracted; prepare a statement from given balances; think: explain why a bank might show a different balance on the same day; pause: after 13.2
sources: no

=== CH14 ===
title: Inventory
purpose: Describe inventory and compare first-in first-out, last-in first-out and weighted average cost.
pace: slow — three cost flow methods must be kept apart
style: mixed
words: 5100
figures: 3
- fig01: layers of inventory by purchase date, with arrows for FIFO and LIFO
- fig02: a three-column comparison of the closing stock value, the goods sold figure and gross profit for each method
- fig03: a timeline of purchases and sales for the textbook
plate: a warehouse interior with stacked crates, sacks and a clerk with a tally board, 1880s
sections:
14.1 | What Inventory Is and Its Types | framework | 325
14.2 | Why Firms Keep Inventory, and Too Much or Too Little | framework | 100
14.3 | FIFO | technique | 650
14.4 | LIFO and Weighted Average | technique | 775
14.5 | Comparing Methods; Income and Tax | framework | 650
concepts:
- 14.1 | Inventory as a current asset | standard | needs: none
- 14.1 | Raw materials, work in process and finished goods | minor | needs: Inventory as a current asset
- 14.2 | Reasons for holding inventory and the dangers of too little or too much | minor | needs: none
- 14.3 | Cost flow and first-in, first-out | core | needs: none
- 14.3 | Ending inventory under FIFO | minor | needs: Cost flow and first-in, first-out
- 14.4 | Last-in, first-out | core | needs: none
- 14.4 | Weighted average cost | standard | needs: Last-in, first-out
- 14.5 | What each method does to profit in rising prices | core | needs: none
- 14.5 | Choosing a method | minor | needs: What each method does to profit in rising prices
defines:
- Inventory | goods a business holds for sale, or materials and part-made goods it holds to make products
- Raw materials | the basic materials a manufacturer buys to make its products
- Work in process | goods that have been started in production but are not yet finished
- Finished goods | completed products waiting to be sold
- Stockout | a shortage that occurs when goods are wanted by customers but none are available
- Cost flow assumption | a rule that decides which purchase costs are assigned to goods sold and which to goods still held
- First-in, first-out (FIFO) | the cost flow assumption that treats the oldest goods as the first sold
- Last-in, first-out (LIFO) | the cost flow assumption that treats the newest goods as the first sold
- Weighted average cost | a method that gives each unit the average cost of all units available
- Ending inventory | the cost of goods still held at the end of the period
assumes: Merchandise inventory, Cost of goods sold, Gross profit, Purchases, Current asset, Income statement, Net income
words-in-use: stock; cost; margin
case: Meghna and Sons, illustrative. October 2024, one title, a first-year Business Mathematics textbook, periodic system. Opening inventory 1 October: 100 units at Tk 400. Purchases: 8 October 200 units at Tk 430; 16 October 150 units at Tk 450; 25 October 50 units at Tk 460. Sales in October: 380 units at Tk 700 each, total Tk 266,000. By code: goods available 500 units, Tk 216,500; ending inventory 120 units. FIFO: ending inventory Tk 54,500; cost of goods sold Tk 162,000; gross profit Tk 104,000. LIFO: ending inventory Tk 48,600; cost of goods sold Tk 167,900; gross profit Tk 98,100. Weighted average cost Tk 433 per unit: ending inventory Tk 51,960; cost of goods sold Tk 164,540; gross profit Tk 101,460. Note: IAS 2 does not permit LIFO, so teach it as a concept and say so.
history: In April 2001 Cisco announced a write-down of about US$2.25 billion on excess inventory after demand for its equipment fell. Search: Cisco April 2001 inventory write-down excess.
refs: Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.1 'Buying and Selling Goods' — cost of goods sold and gross profit, defined earlier; Chapter 15, 'Plant Assets and Depreciation', section 15.2 'Why We Depreciate; Factors That Affect It' — another place where a choice of method changes profit
need: Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.1 'Buying and Selling Goods'; Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.3 'The Classified Income Statement'
ladder: 1) two purchases and one sale at clean prices; 2) three purchases and two sales, FIFO only; 3) the October textbook under all three methods; 4) a new product with falling prices and a comparison of the three profit figures.
practice: review: work out the value of goods left and the cost of goods sold for each of the three methods; say which method gives the highest profit when prices rise and why; think: advise a firm on which method to choose, giving two reasons; pause: after 14.3 and 14.4
sources: no

=== CH15 ===
title: Plant Assets and Depreciation
purpose: Teach the cost of a plant asset, why it is depreciated, three methods, and the entries when it is sold.
pace: slow — three depreciation methods and a disposal
style: mixed
words: 5325
figures: 3
- fig01: three bar charts of yearly depreciation under the three methods
- fig02: book value falling year by year on one axis
- fig03: a depreciation schedule table
plate: a steam-driven printing press with a mechanic oiling its wheels, 1880s
sections:
15.1 | Nature and Cost of Plant Assets | framework | 325
15.2 | Why We Depreciate; Factors That Affect It | new idea | 650
15.3 | Straight-Line and Units of Production | technique | 775
15.4 | Sum of the Years' Digits | technique | 325
15.5 | Schedules, Disposal and Statement Presentation | technique | 650
concepts:
- 15.1 | What a plant asset is | standard | needs: none
- 15.1 | What goes into its cost | minor | needs: What a plant asset is
- 15.2 | Useful life, residual value and depreciable cost | core | needs: none
- 15.2 | Depreciation expense versus accumulated depreciation | minor | needs: Useful life, residual value and depreciable cost
- 15.3 | Straight-line method | core | needs: none
- 15.3 | Units-of-production method | standard | needs: Straight-line method
- 15.4 | Sum-of-the-years'-digits method | standard | needs: none
- 15.4 | Comparing the three patterns | minor | needs: Sum-of-the-years'-digits method
- 15.5 | Depreciation schedule and balance sheet presentation | core | needs: none
- 15.5 | Selling a plant asset at a gain or a loss | minor | needs: Depreciation schedule and balance sheet presentation
defines:
- Plant asset | a long-lived physical asset, such as equipment or a building, used in running the business
- Capital expenditure | spending that adds to the cost of an asset, including delivery and installation
- Useful life | the period over which an asset is expected to be of use to the business
- Residual value | the amount the firm expects to receive when it disposes of the asset at the end of its useful life
- Depreciable cost | the cost of an asset less its residual value
- Straight-line method | a method that charges the same depreciation each year
- Units-of-production method | a method that charges depreciation in proportion to how much the asset is used
- Sum-of-the-years'-digits method | a method that charges more depreciation in early years, using a falling fraction of depreciable cost
- Book value | an asset's cost less its accumulated depreciation
- Depreciation schedule | a table showing the depreciation, accumulated depreciation and book value for each year
assumes: Depreciation, Accumulated depreciation, Contra account, Adjusting entry, Non-current asset, Balance sheet, Journal entry
words-in-use: capital; plant; charge
case: Meghna and Sons, illustrative. On 1 January 2023 the firm bought an automatic binding machine for Tk 480,000 and paid Tk 20,000 for delivery and installation, total cost Tk 500,000. Useful life 5 years; residual value Tk 50,000; depreciable cost Tk 450,000. By code, straight-line Tk 90,000 a year. Sum of the years' digits (15): Tk 150,000; Tk 120,000; Tk 90,000; Tk 60,000; Tk 30,000. Units of production: expected output 900,000 books bound, Tk 0.50 a book; output 200,000 in 2023, 250,000 in 2024, 180,000 in 2025, giving Tk 100,000; Tk 125,000; Tk 90,000. Under straight-line, accumulated depreciation at 31 December 2025 is Tk 270,000 and book value Tk 230,000. The machine was sold on 31 December 2025 for Tk 190,000, a loss of Tk 40,000.
history: In 1998 the waste company Waste Management restated years of earnings after it was found that useful lives of its vehicles and containers had been extended without good reason. Search: Waste Management 1998 restatement depreciation useful lives SEC.
refs: Chapter 8, 'Adjusting the Accounts', section 8.4 'Depreciation as an Adjustment' — depreciation first met as an adjustment; Chapter 14, 'Inventory', section 14.5 'Comparing Methods; Income and Tax' — another choice of method that shifts profit
need: Chapter 8, 'Adjusting the Accounts', section 8.4 'Depreciation as an Adjustment'; Chapter 11, 'Merchandising Company Accounts and Classified Statements', section 11.4 'The Classified Balance Sheet'
ladder: 1) one machine, straight-line, round figures; 2) the same machine under units of production; 3) the binding machine under all three methods with a schedule; 4) a disposal at a gain and at a loss with balance sheet presentation.
practice: review: compute depreciation by each method; prepare the journal entry for a sale; think: explain why total depreciation over the whole life is the same whichever method is chosen; pause: after 15.2 and 15.3
sources: no

=== CH16 ===
title: Non-Trading Concerns and Partnership Accounts
purpose: Show the accounts of a club that does not trade for profit and the accounts of a partnership.
pace: standard — two new organisation types, each with its own accounts
style: mixed
words: 4675
figures: 2
- fig01: a receipts and payments account converted into an income and expenditure account
- fig02: the order of a profit appropriation account
plate: two partners shaking hands over a desk with a sealed document between them, 1880s
sections:
16.1 | Non-Trading Concerns | framework | 650
16.2 | Forming a Partnership and the Deed | framework | 650
16.3 | Sharing Profit and Partners' Capital | technique | 775
concepts:
- 16.1 | Receipts and payments account | core | needs: none
- 16.1 | Income and expenditure account and surplus | minor | needs: Receipts and payments account
- 16.2 | Features of a partnership | core | needs: none
- 16.2 | Contents of a partnership deed | minor | needs: Features of a partnership
- 16.3 | Profit-sharing ratio, interest and salary | core | needs: none
- 16.3 | The appropriation account and partners' balances | standard | needs: Profit-sharing ratio, interest and salary
defines:
- Non-trading concern | an organisation, such as a club, that exists to serve its members and not to earn profit
- Receipts and payments account | a summary of all cash received and paid in a period, whatever period it belongs to
- Income and expenditure account | the report of a non-trading concern that matches income and costs to the period, like an income statement
- Surplus | the amount by which income is greater than expenditure in a non-trading concern
- Deficit | the amount by which expenditure is greater than income in a non-trading concern
- Subscription | a regular payment that a member makes to a club
- Partnership deed | the written agreement among partners on how the business is run and profit shared
- Profit-sharing ratio | the agreed proportions in which partners share profit and loss
- Interest on capital | an agreed payment to a partner for the capital put into the business
- Appropriation account | the account that shows how a partnership's profit is divided among the partners
assumes: Partnership, Owner's equity, Net income, Income statement, Accrued expense, Unearned revenue, Prepaid expense, Drawings, Accrual basis
words-in-use: club; deed; share
case: Meghna and Sons, illustrative. Club: the Meghna Readers' Club, begun by the family in 2023. Receipts and payments for the year ended 31 December 2024: opening cash Tk 15,000; subscriptions received Tk 84,000; donations Tk 20,000; sale of old books Tk 9,000; payments for hall rent Tk 36,000, newspapers and magazines Tk 12,000, new books Tk 18,000, librarian's salary Tk 24,000, refreshments Tk 7,000. Closing cash Tk 31,000. Adjustments: subscriptions owing for 2024 Tk 4,000; subscriptions received in advance for 2025 Tk 6,000; hall rent owing Tk 3,000. By code: income Tk 111,000; expenditure Tk 100,000; surplus Tk 11,000. Partnership: from 1 January 2025 Karim Meghna and his son Imran Meghna are partners. Capital: Karim Tk 600,000; Imran Tk 300,000. Terms: interest on capital 5% a year; salary to Imran Tk 60,000; the rest shared 2:1 (Karim:Imran). Profit before appropriation for 2025 Tk 420,000. By code: interest Karim Tk 30,000, Imran Tk 15,000; remainder Tk 315,000, Karim Tk 210,000, Imran Tk 105,000; totals Karim Tk 240,000, Imran Tk 180,000. Drawings: Karim Tk 90,000; Imran Tk 60,000. Closing balances Karim Tk 750,000; Imran Tk 420,000.
history: BRAC, a non-profit organisation, was founded in 1972 by Fazle Hasan Abed to help refugees returning to Bangladesh after the war, and became one of the world's largest non-governmental organisations. Search: BRAC founded 1972 Fazle Hasan Abed Sulla.
refs: Chapter 8, 'Adjusting the Accounts', section 8.1 'Why Accounts Need Adjusting' — accrual adjustments applied to club accounts; Chapter 17, 'Partnership Liquidation', section 17.1 'What Liquidation Means and Why It Happens' — what happens when a partnership ends
need: Chapter 8, 'Adjusting the Accounts', section 8.2 'Prepaid Items and Unearned Revenue'; Chapter 8, 'Adjusting the Accounts', section 8.3 'Accrued Items'; Chapter 1, 'Business, Money and Records', section 1.4 'Sole Trader, Partnership and Company'
ladder: 1) a receipts and payments account for a stall club; 2) the same account with one accrued item; 3) the readers' club with three adjustments; 4) a partnership with interest, salary and a 2:1 split.
practice: review: convert a receipts and payments account into an income and expenditure account; divide a profit among partners; think: explain why a club has a surplus and not a profit; pause: after 16.1
sources: no

=== CH17 ===
title: Partnership Liquidation
purpose: Teach what happens when a partnership ends: selling assets, paying creditors and sharing out cash.
pace: slow — several assumptions in turn, each with its own distribution
style: calculation
words: 4125
figures: 2
- fig01: the order of payment in a liquidation as a stair of three steps
- fig02: a cash distribution schedule with a column for each partner
plate: an auctioneer with a gavel in a half-empty warehouse, a few buyers in top hats, 1880s
sections:
17.1 | What Liquidation Means and Why It Happens | framework | 100
17.2 | Selling Assets and Paying Creditors | technique | 650
17.3 | Distributing Cash to Partners | technique | 775
concepts:
- 17.1 | Liquidation and the reasons partnerships end | minor | needs: none
- 17.2 | Realisation of non-cash assets and the loss on realisation | core | needs: none
- 17.2 | Paying liabilities before partners | minor | needs: Realisation of non-cash assets and the loss on realisation
- 17.3 | Closing partners' capital and the cash distribution schedule | core | needs: none
- 17.3 | When a partner has a capital deficiency | standard | needs: Closing partners' capital and the cash distribution schedule
defines:
- Liquidation | the process of selling a business's assets, paying its debts and sharing what is left among the owners
- Realisation | the sale of the assets of a business for cash
- Capital deficiency | a debit balance in a partner's capital account after losses are shared
- Cash distribution schedule | a table that shows how cash is paid out to creditors and partners step by step
assumes: Partnership, Partnership deed, Profit-sharing ratio, Liability, Asset, Journal entry, Owner's equity, Appropriation account
words-in-use: loss; deficiency
case: Meghna and Sons, illustrative. A planning exercise on 31 March 2026: the partners Karim and Imran Meghna study what would happen if the partnership were closed. Balance sheet: cash Tk 100,000; non-cash assets Tk 800,000; liabilities Tk 300,000; capital Karim Tk 450,000 and Imran Tk 150,000 (Tk 900,000 each side). Losses are shared 2:1. By code: (A) non-cash assets sold for Tk 590,000, loss Tk 210,000 (Karim Tk 140,000; Imran Tk 70,000); cash Tk 690,000, after paying liabilities Tk 390,000 is shared: Karim Tk 310,000; Imran Tk 80,000. (B) assets sold for Tk 320,000, loss Tk 480,000 (Karim Tk 320,000; Imran Tk 160,000); Imran's capital falls to a deficiency of Tk 10,000, which he pays in cash, so Karim receives Tk 130,000. (C) as (B) but Imran cannot pay; Karim absorbs the Tk 10,000 and receives Tk 120,000. The firm in fact continued.
history: Arthur Andersen, one of the world's largest accounting partnerships, wound down in 2002 after its conviction for obstruction of justice linked to the Enron audit. Search: Arthur Andersen 2002 conviction wind-down partnership.
refs: Chapter 16, 'Non-Trading Concerns and Partnership Accounts', section 16.3 'Sharing Profit and Partners' Capital' — how profits and losses are shared among partners
need: Chapter 16, 'Non-Trading Concerns and Partnership Accounts', section 16.2 'Forming a Partnership and the Deed'; Chapter 16, 'Non-Trading Concerns and Partnership Accounts', section 16.3 'Sharing Profit and Partners' Capital'
ladder: 1) a firm sells every asset for exactly its book value; 2) a sale at a loss shared 2:1; 3) a sale in which one partner's capital turns negative and he pays; 4) the same sale when he cannot pay.
practice: review: write the entries for selling assets, paying creditors and paying partners; build a distribution schedule; think: explain why creditors are paid before partners; pause: after 17.2
sources: no

=== CH18 ===
title: Company Accounting and Shares
purpose: Introduce the company form, its types of share, and the entries for issuing shares.
pace: standard — new vocabulary on a familiar base
style: mixed
words: 3900
figures: 2
- fig01: owners, shares and company shown as three layers
- fig02: the stages of issuing a share, with the amount due at each stage
plate: a stock exchange floor with merchants in top hats exchanging paper certificates, 1890s
sections:
18.1 | What a Company Is | framework | 325
18.2 | Types of Shares | framework | 325
18.3 | Issuing Shares | technique | 650
concepts:
- 18.1 | The company as a separate legal person | standard | needs: none
- 18.1 | Limited liability | minor | needs: The company as a separate legal person
- 18.2 | Ordinary and preference shares | standard | needs: none
- 18.2 | Par value and share premium | minor | needs: Ordinary and preference shares
- 18.3 | Application, allotment and calls | core | needs: none
- 18.3 | Journal entries for each stage | minor | needs: Application, allotment and calls
defines:
- Share | one of the equal parts into which a company's capital is divided
- Shareholder | a person or organisation that owns one or more shares in a company
- Limited liability | the rule that shareholders can lose no more than they have paid or agreed to pay for their shares
- Ordinary share | a share that carries the right to vote and to receive the profit left after other claims
- Preference share | a share that has a right to a fixed dividend before ordinary shareholders are paid
- Par value | the face value printed on a share
- Share premium | the amount a company receives above par value when it issues a share
- Dividend | a share of a company's profit paid to its shareholders
- Application money | the first payment, made with a request to buy shares
- Allotment | the company's decision to give shares to applicants, with the payment due on that step
- Call | a later request to shareholders to pay part of the amount still owed on their shares
assumes: Company, Owner, Owner's equity, Journal entry, Debit, Credit, Partnership, Profit
words-in-use: share; call; par
case: Meghna and Sons, illustrative. On 1 July 2026 the family business became Meghna Books Limited. Authorised capital Tk 6,000,000: 400,000 ordinary shares of Tk 10 par value and 20,000 6% preference shares of Tk 100 par value. Issue of 200,000 ordinary shares at Tk 12 each, payable Tk 4 on application, Tk 5 on allotment (including the Tk 2 premium) and Tk 3 on the final call. By code: application Tk 800,000; allotment Tk 1,000,000; call Tk 600,000; total Tk 2,400,000, of which share capital Tk 2,000,000 and share premium Tk 400,000. All applicants pay in full on each due date. 20,000 preference shares issued at par for cash, Tk 2,000,000.
history: The Dhaka Stock Exchange was established in 1954 as the East Pakistan Stock Exchange Association and renamed in 1964. Search: Dhaka Stock Exchange history 1954 established.
refs: Chapter 16, 'Non-Trading Concerns and Partnership Accounts', section 16.2 'Forming a Partnership and the Deed' — the partnership form that the company replaces; Chapter 1, 'Business, Money and Records', section 1.4 'Sole Trader, Partnership and Company' — the three forms of ownership first introduced
need: Chapter 1, 'Business, Money and Records', section 1.4 'Sole Trader, Partnership and Company'; Chapter 5, 'Accounts, Debits and Credits', section 5.3 'Double Entry in Practice'; Chapter 6, 'Journal and Ledger', section 6.1 'The Journal and Journal Entries'
ladder: 1) one share issued at par for cash; 2) the same issue in three instalments; 3) an issue at a premium with application, allotment and call; 4) the company's full opening entries, ordinary and preference.
practice: review: tell ordinary and preference shares apart; write the entries for each stage of an issue; think: explain why a shareholder's loss is limited and a sole trader's is not; pause: after 18.2
sources: no

=== A1 ===
title: Maths You Will Use
purpose: Give a short refresher of the arithmetic and algebra the chapters use.
pace: standard — a reference to dip into, not a lesson
style: calculation
words: 1000
figures: 0
sections:
A1.1 | Percentages and Percentage Change | technique | 350
A1.2 | Ratios and Averages | technique | 350
A1.3 | Rearranging, Rounding and Graphs | technique | 300
concepts:
- A1.1 | Percentage, percentage of a number and percentage change | standard | needs: none
- A1.2 | Ratio, sharing in a ratio, and the average | standard | needs: none
- A1.3 | Rearranging an equation, rounding, and reading a graph | standard | needs: none
defines:
- Percentage | a number written as a part out of one hundred
- Percentage change | the size of an increase or decrease shown as a percentage of the starting figure
- Ratio | a comparison of two or more amounts, written with a colon, such as 2:1
- Average | the total of a set of numbers divided by how many numbers there are
- Rounding | replacing a number by a nearby simpler number, such as the nearest whole taka
assumes: none
words-in-use: none
case: none
history: none
refs: Chapter 3, 'The Accounting Equation', section 3.4 'Summarising Transactions in the Equation' — first equations in the book; Chapter 14, 'Inventory', section 14.4 'LIFO and Weighted Average' — averages used in weighted average cost; Chapter 15, 'Plant Assets and Depreciation', section 15.3 'Straight-Line and Units of Production' — sharing and fractions in depreciation
need: nothing
ladder: 1) a percentage of a price; 2) a percentage change between two years; 3) sharing profit in a ratio; 4) rearranging an equation and rounding to the nearest taka.
practice: review: three or four short exercises per topic with answers; think: none; pause: none
sources: no
