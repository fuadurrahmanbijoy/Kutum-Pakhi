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
course: MGT 104
book: MGT 104
spelling: British · dates: day, month, year (12 March 2026) · country: mixed, no single country; the running case's home is Bangladesh, but examples and history draw on several countries; name the place whenever law or standards differ · currency and numbers: taka for the running case, written Tk 158,000 (international digit grouping); a historical case keeps its own currency
running case: Meghna and Sons, a family-run bookshop in Dhaka, shown as an illustrative documented case file — illustrative. Base facts (FIXED): opened 4 January 2004 by Abdul Meghna; in 2026 run by his daughter Shirin Meghna and his son Imran Meghna; one shop of 600 square feet; two paid assistants; shop rent Tk 60,000 a month; a binding corner for theses added 3 March 2026. Chapter slices are fixed in each entry; no dialogue and no invented feelings.
chosen words (one term, one word):
- use firm — also called business, enterprise
- use good — also called commodity, product
- use consumer surplus — also called consumers' surplus
- use price elasticity of demand — also called elasticity of demand
- use law of diminishing returns — also called law of variable proportions
- use economic rent — also called pure rent
- use wage — also called wage rate
- use rate of interest — also called interest rate
- use economic organisation — also called economic unit
size plan: 12 chapters and appendix A1, ~56,800 words, ~241 pages
chapters:
1. Scarcity, Choice and the Economic Problem
2. Economic Reasoning, Laws and the Scope of Microeconomics
3. Utility and Diminishing Marginal Utility
4. Demand and the Demand Curve
5. Elasticity of Demand
6. Consumer Choice: Surplus and Indifference Curves
7. Supply and Elasticity of Supply
8. How Markets Find a Price
9. Production
10. Costs of Production
11. Market Structures and the Firm
12. Distribution: Rent, Wages, Interest and Profit
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
title: Scarcity, Choice and the Economic Problem
purpose: Show why every society and every shop must choose, and give the reader the first working words of economics.
pace: slow — first chapter; teaches how to read the book as well as the subject
style: descriptive
words: 4700
figures: 1
- fig01: a pair of bars comparing the forgone return of two stock choices, with the chosen option marked
plate: a clerk at a high desk among ledgers, 1880s
sections:
1.1 | Wants, Resources and Scarcity | new idea | 775
1.2 | Choice and Opportunity Cost | new idea | 550
1.3 | The Basic Problems of an Economic Organisation | framework | 550
1.4 | Defining Economics | defining theory | 225
concepts:
- 1.1 | scarcity: limited resources against wants without limit | core | needs: none
- 1.1 | wants, resources and the factors of production | standard | needs: none
- 1.2 | opportunity cost: the value of the best option given up | core | needs: 1.1 scarcity
- 1.3 | what, how and for whom: the three problems every economy answers | core | needs: 1.2 opportunity cost
- 1.4 | how economists have defined their subject, and the definition this book uses | standard | needs: 1.1 scarcity; 1.2 opportunity cost
defines:
- Economics | the study of how people, firms and societies choose among uses of limited resources to meet wants
- Want | something a person would like to have, whether or not they can pay for it
- Resource | anything used to make goods and services: land, labour, capital and enterprise
- Factor of production | one of the four kinds of resource used in making things: land, labour, capital, enterprise
- Good | a physical thing people buy to satisfy a want, such as a book or a pen
- Service | an activity done for someone, such as binding a thesis or delivering parcels
- Scarcity | the condition in which resources are too few to satisfy all the wants people have
- Choice | picking one option and giving up the others because resources cannot cover every option
- Opportunity cost | the value of the best alternative given up when a choice is made
- Firm | an organisation that uses resources to make goods or services and sell them
- Household | a person or group living together that buys goods and services and supplies resources
- Economic organisation | the way a society or business arranges who decides what is made, how and for whom
- Economic system | the set of rules and institutions a country uses to answer its basic economic problems
assumes: nothing
words-in-use: scarce; cost; system
case: Meghna and Sons is an illustrative documented case file. Base facts (FIXED): a bookshop in Dhaka opened on 4 January 2004 by Abdul Meghna; in 2026 run by his daughter Shirin Meghna and his son Imran Meghna; one shop of 600 square feet; two paid assistants. Record of 12 January 2026: restock fund Tk 400,000 in cash from family savings; shelf space allows one large restock only. Option A, textbooks: purchase cost Tk 400,000; expected sales Tk 560,000; expected sales less purchase cost Tk 160,000. Option B, stationery: purchase cost Tk 400,000; expected sales Tk 540,000; expected sales less purchase cost Tk 140,000. Decision recorded: option A. Opportunity cost of that decision: Tk 140,000. The three problems in shop terms: what to stock (textbooks), how to run the shop (family at the counter plus two assistants), for whom (university students first, schools second).
history: US petrol shortage after the October 1973 oil embargo, with queues and the odd-even plate rationing of 1974; search: 1973 oil embargo gasoline lines odd-even rationing
refs: none
need: nothing
ladder: familiar case (the shop's two stock options); reshaped case (a household choosing between a phone plan and school fees); new setting (a village deciding between a road and a clinic); combined case (a firm choosing what, how and for whom under one budget)
practice: review: scarcity versus shortage, forgone value of a choice made from a new price list, which of the three problems a given decision belongs to; think: a student has Tk 9,000 and one free Saturday and must pick between two paid tasks and a course fee — name the opportunity cost; pause: after the scarcity passage and after the opportunity-cost passage
sources: yes


=== CH02 ===
title: Economic Reasoning, Laws and the Scope of Microeconomics
purpose: Teach the reader how economists argue, what an economic law is, and where microeconomics fits.
pace: slow — second chapter; sets the habits of reasoning used throughout
style: descriptive
words: 4600
figures: 1
- fig01: a two-branch map of economics showing the questions that belong to microeconomics and to macroeconomics
plate: a lecture-hall demonstrator beside a brass orrery and a slate board, 1880s
sections:
2.1 | Science, Art and Normative Views | new idea | 550
2.2 | Economic Laws | new idea | 550
2.3 | Microeconomics and Macroeconomics | framework | 450
2.4 | Scope, Importance and Objectives | framework | 450
concepts:
- 2.1 | positive and normative statements, set within the question of whether economics is a science or an art | core | needs: 1.4 the definition used in this book
- 2.2 | economic law as a tendency that holds when other things are equal | core | needs: none
- 2.3 | microeconomics: choices of single households, firms and markets | standard | needs: none
- 2.3 | macroeconomics and the link between the two | standard | needs: 2.3 microeconomics
- 2.4 | scope and importance of microeconomics | standard | needs: 2.3 microeconomics
- 2.4 | objectives of studying it and prospects in Bangladesh, with the institutions that support its use | standard | needs: 2.3 microeconomics
defines:
- Science | a body of knowledge built by observing facts, forming explanations and testing them
- Art | the skilled use of knowledge to reach a practical aim
- Positive statement | a claim about what is, which can be checked against facts
- Normative statement | a claim about what ought to be, resting on values and opinion
- Ceteris paribus | a Latin phrase meaning other things being equal, used to study one change at a time
- Economic law | a statement of a regular tendency in human choices, true when other things stay equal
- Model | a simplified picture of a situation that keeps only the features needed to answer a question
- Microeconomics | the study of choices made by single households, firms and markets
- Macroeconomics | the study of the economy as a whole, such as total output, jobs and the general price level
assumes: Economics; Scarcity; Choice; Firm; Household; Economic system
words-in-use: law; model; science
case: Meghna and Sons (illustrative). Base facts carried: bookshop in Dhaka, run in 2026 by Shirin and Imran Meghna, restock decision of 12 January 2026 (Chapter 1 facts need not be repeated beyond this). Records of 5 February 2026: a 200-page exercise book sells at Tk 60 and 200 copies sell in a week. Ledger note A, in Shirin Meghna's hand: when the price was raised to Tk 66 on 2 March 2026, weekly sales fell to 188. Ledger note B, in Imran Meghna's hand: students should not have to pay more than Tk 60. Note A can be checked against sales records; note B cannot. Regular tendency recorded over three years: textbook sales rise in the two weeks before each term begins (this holds when the shop's prices stay unchanged). Micro and macro: the shop's price and stock are micro matters; the movement of the average price of all goods in Bangladesh is a macro matter.
history: Great Debasement under Henry VIII, 1544 to 1551, and Thomas Gresham's observation about money; search: Great Debasement Gresham's law
refs: Chapter 1, 'Scarcity, Choice and the Economic Problem', section 1.4 'Defining Economics' — the definition the reader now tests against science and art
need: Chapter 1 sections 1.1 to 1.4
ladder: familiar case (the shop's two ledger notes); reshaped case (a bus company's claims about fares); new setting (a school's claims about exam fees, kept free of any real exam paper); combined case (a statement mixing fact and opinion to be separated)
practice: review: sort five statements into positive and normative, state a law with its other-things-equal condition, place four decisions under micro or macro; think: a minister says bread should be cheaper — separate the checkable part from the opinion; pause: after the other-things-equal passage and after the micro-macro split
sources: no


=== CH03 ===
title: Utility and Diminishing Marginal Utility
purpose: Explain satisfaction as the root of demand and give the first law the reader can test.
pace: slow — third chapter; first use of schedules and a law with a diagram
style: mixed
words: 4600
figures: 3
- fig01: the total utility curve rising and flattening against units consumed
- fig02: the marginal utility curve falling to zero against the same units
- fig03: one panel pairing total and marginal utility so the reader sees their link
plate: a still life of a loaf, a cup and a spoon on a worn kitchen table, 1880s
sections:
3.1 | Utility and Satisfaction | new idea | 775
3.2 | The Law of Diminishing Marginal Utility | defining theory | 775
3.3 | Limitations of the Law | framework | 450
concepts:
- 3.1 | utility, total utility and marginal utility | core | needs: 1.1 scarcity
- 3.1 | whether satisfaction can be measured: cardinal and ordinal views | standard | needs: 3.1 utility
- 3.2 | the law itself, with schedule and diagram | core | needs: 3.1 utility
- 3.2 | why marginal utility falls | standard | needs: 3.2 the law
- 3.3 | the conditions the law needs | standard | needs: 3.2 the law
- 3.3 | cases where the law seems to fail | standard | needs: 3.2 the law
defines:
- Utility | the satisfaction a person gets from using a good or service
- Consumer | a person who buys or uses goods and services to meet wants
- Total utility | the whole satisfaction from all the units of a good consumed in a period
- Marginal utility | the extra satisfaction gained from consuming one more unit of a good
- Util | an imaginary unit used to count satisfaction in examples
- Cardinal measurement | measuring satisfaction in numbers, such as 20 utils, so amounts can be added and compared
- Ordinal measurement | ranking satisfaction as first, second and third without giving it a number
- Law of diminishing marginal utility | as a person consumes more units of a good, the extra satisfaction from each further unit falls
- Saturation point | the quantity at which marginal utility reaches zero and total utility stops rising
assumes: Want; Scarcity; Choice; Ceteris paribus; Economic law
words-in-use: utility; marginal; satisfaction
case: Meghna and Sons (illustrative). Survey card of 10 February 2026 for one regular customer, satisfaction scored in utils for notebooks bought in one visit: first notebook 20 utils, second 14, third 9, fourth 5, fifth 2. Derived (by code in the writer's check): total utility 20, 34, 43, 48, 50; marginal utility 20, 14, 9, 5, 2. A sixth notebook is rated 0 and a seventh would lower satisfaction by 3. Conditions noted on the card: all notebooks of the same kind, bought in a single visit, no change in taste. Notebook price Tk 60 (carried from the shop's price list).
history: The marginal revolution of 1871 to 1874: Jevons, Menger and Walras explain the diamond-and-water puzzle; search: marginal revolution 1871 Jevons Menger diamond water paradox
refs: Chapter 2, 'Economic Reasoning, Laws and the Scope of Microeconomics', section 2.2 'Economic Laws' — a law holds only when other things are equal
need: Chapter 2 section 2.2 'Economic Laws'
ladder: familiar case (the five notebooks); reshaped case (cups of tea at a stall); new setting (rounds of a free-to-play game); combined case (a table with a missing column to complete and read)
practice: review: complete a total-and-marginal table from new scores, state the law with its conditions, give one apparent exception and say why it is not one; think: a diner eats from a buffet — find where marginal utility reaches zero and say what a sensible diner does next; pause: after the total-versus-marginal passage and after the reasons-it-falls passage
sources: yes


=== CH04 ===
title: Demand and the Demand Curve
purpose: Build the demand idea from a price table to a curve, and show what moves along it and what shifts it.
pace: standard — builds directly on utility and on the curve-reading practice of the earlier chapters
style: descriptive
words: 4600
figures: 4
- fig01: a demand curve drawn from the exercise-book schedule
- fig02: a movement along the curve set beside a shift of the whole curve
- fig03: a rightward and a leftward shift with the causes labelled
- fig04: the curve of an exceptional good that bends upward, with the snob and bandwagon cases beside it
plate: a market-day crowd under a covered market hall with a painted price board, 1880s
sections:
4.1 | What Demand Means | new idea | 450
4.2 | The Law of Demand | defining theory | 550
4.3 | What Moves the Demand Curve | new idea | 550
4.4 | Related Goods and Exceptions | new idea | 450
concepts:
- 4.1 | demand, quantity demanded and the demand schedule | standard | needs: 3.1 utility
- 4.1 | individual and market demand; the meaning of a market | standard | needs: 4.1 demand
- 4.2 | the law of demand and why the curve slopes down | core | needs: 3.2 the law of diminishing marginal utility; 4.1 demand
- 4.3 | determinants of demand; movement along the curve versus a shift of the curve | core | needs: 4.2 the law
- 4.4 | substitutes and complements, and what a price change in one does to demand for the other | standard | needs: 4.3 determinants
- 4.4 | exceptions: Giffen goods, snob effect, bandwagon effect | standard | needs: 4.2 the law
defines:
- Demand | the quantity of a good people are willing and able to buy at each possible price, in a given period
- Quantity demanded | the amount people plan to buy at one particular price
- Demand schedule | a table listing the quantity demanded at each of several prices
- Demand curve | a line on a graph showing the quantity demanded at each price, other things equal
- Market | any arrangement that brings buyers and sellers of a good together
- Market demand | the sum of all individual buyers' demands for a good at each price
- Law of demand | when the price of a good rises, quantity demanded falls, and when it falls, quantity demanded rises, other things equal
- Determinants of demand | the things other than the good's own price that change how much people want to buy
- Normal good | a good for which demand rises when buyers' incomes rise
- Inferior good | a good for which demand falls when buyers' incomes rise
- Substitute goods | goods that can replace each other, so a rise in one's price raises demand for the other
- Complementary goods | goods used together, so a rise in one's price lowers demand for the other
- Giffen good | a rare inferior good for which a price rise leads buyers to buy more of it
- Snob effect | a fall in demand for a good because more people begin to own it
- Bandwagon effect | a rise in demand for a good because more people are seen to buy it
assumes: Utility; Marginal utility; Law of diminishing marginal utility; Consumer; Ceteris paribus
words-in-use: demand; market; curve
case: Meghna and Sons (illustrative). Five-week trial from 26 January to 27 February 2026, one price per week, 200-page exercise book. Weekly sales: Tk 50, 240 copies; Tk 55, 220; Tk 60, 200; Tk 66, 188; Tk 70, 180. Shock to determinants: schools announced a drawing term on 10 March 2026, and weekly sales at Tk 60 rose from 200 to 230 (a shift of the curve). Complements: when pen-pack price was cut from Tk 100 to Tk 90 on 16 March 2026, notebook sales at Tk 60 rose from 200 to 210 a week. Substitutes: when the price of a second-hand prescribed textbook fell by 20 per cent, weekly sales of the new copy fell from 50 to 44 (new copy price Tk 700). Snob effect: a numbered edition at Tk 2,400 sold out in three days, while the unnumbered Tk 1,200 edition took three weeks. Bandwagon effect: a title at Tk 450 sold 20 copies a week until it topped a public bestseller list, then 85 a week. Giffen good: no case in the shop; explain only in general terms.
history: Gregory King's table of harvest shortfalls and wheat prices, published by Charles Davenant in 1699; search: Gregory King Davenant 1699 harvest wheat price
refs: Chapter 3, 'Utility and Diminishing Marginal Utility', section 3.2 'The Law of Diminishing Marginal Utility' — falling marginal utility is why a buyer will pay less for each extra unit
need: Chapter 3 section 3.2 'The Law of Diminishing Marginal Utility'
ladder: familiar case (the exercise-book trial); reshaped case (bus tickets on a route); new setting (bottled water at a cricket ground); combined case (a price table with a shift caused by a related good)
practice: review: draw a curve from a new schedule, tell a movement from a shift in five events, say how a pen-pack price change affects notebook demand; think: when the price of petrol rises, say what probably happens to demand for natural gas and why; pause: after the movement-versus-shift passage and after the exceptions passage
sources: no


=== CH05 ===
title: Elasticity of Demand
purpose: Teach how to measure how strongly buyers respond, with percentages, and what the answer means for revenue.
pace: standard — numeric but each step is small
style: calculation
words: 4600
figures: 4
- fig01: a steep and a flat demand curve side by side for the same price change
- fig02: five demand curves for the five forms of price elasticity
- fig03: total revenue before and after a price rise for an inelastic and an elastic good
- fig04: a number line placing income elasticity values for necessities, comforts and luxuries
plate: a laboratory spring balance with brass weights on a draper's counter, 1880s
sections:
5.1 | Measuring Responsiveness | technique | 775
5.2 | Forms of Price Elasticity | new idea | 450
5.3 | What Affects Price Elasticity | new idea | 225
5.4 | Income and Cross Elasticity | technique | 550
concepts:
- 5.1 | price elasticity of demand and its percentage formula | core | needs: 4.2 the law of demand
- 5.1 | percentage change and the midpoint approach | standard | needs: 5.1 price elasticity
- 5.2 | elastic, inelastic, unit elastic, perfectly elastic and perfectly inelastic demand | standard | needs: 5.1 price elasticity
- 5.2 | total revenue and elasticity | standard | needs: 5.2 forms
- 5.3 | availability of substitutes, share of income, time and necessity | standard | needs: 4.4 substitute goods
- 5.4 | income elasticity of demand and cross elasticity of demand | core | needs: 4.3 determinants of demand; 5.1 price elasticity
defines:
- Elasticity | a measure of how strongly one quantity responds when another quantity changes
- Percentage change | the size of a change divided by the starting value, multiplied by 100
- Price elasticity of demand | the percentage change in quantity demanded divided by the percentage change in price
- Elastic demand | demand for which the percentage fall in quantity is greater than the percentage rise in price
- Inelastic demand | demand for which the percentage fall in quantity is smaller than the percentage rise in price
- Unit elastic demand | demand for which the percentage change in quantity equals the percentage change in price
- Perfectly elastic demand | demand that vanishes completely for any price rise, however small, shown as a flat curve
- Perfectly inelastic demand | demand that does not change at all when price changes, shown as a vertical curve
- Total revenue | the money a seller receives from sales, found by price multiplied by quantity sold
- Income elasticity of demand | the percentage change in quantity demanded divided by the percentage change in buyers' income
- Cross elasticity of demand | the percentage change in quantity demanded of one good divided by the percentage change in another good's price
assumes: Demand; Quantity demanded; Demand curve; Determinants of demand; Substitute goods; Normal good; Inferior good
words-in-use: necessity; luxury; responsive
case: Meghna and Sons (illustrative). Price elasticity: 200-page exercise book, price rose from Tk 60 to Tk 66 on 2 March 2026; weekly sales fell from 200 to 188. Clean figures: price change +10 per cent, quantity change -6 per cent, elasticity 0.6 (inelastic); total revenue Tk 12,000 (60 x 200) to Tk 12,408 (66 x 188). Messier rung: midpoint method gives about 0.65. Second good: a Tk 300 atlas, price cut to Tk 270 raised weekly sales from 20 to 30: -10 per cent price, +50 per cent quantity, elasticity 5 in size (elastic); revenue Tk 6,000 to Tk 8,100. Income elasticity: a household income rose from Tk 30,000 to Tk 33,000 a month and its novels bought rose from 50 to 60 a year: +10 per cent and +20 per cent, elasticity 2. Cross elasticity: a rival shop raised its notebook price from Tk 50 to Tk 55 (+10 per cent) and Meghna and Sons sales of its own notebooks rose from 100 to 108 a week (+8 per cent), cross elasticity 0.8.
history: Alfred Marshall introduces elasticity of demand in Principles of Economics, 1890; search: Marshall Principles of Economics 1890 elasticity of demand origin
refs: Chapter 4, 'Demand and the Demand Curve', section 4.2 'The Law of Demand' — the price and quantity link measured here; Chapter 4 section 4.4 'Related Goods and Exceptions' — substitutes and complements behind cross elasticity
need: Chapter 4 sections 4.2 'The Law of Demand' and 4.4 'Related Goods and Exceptions'
ladder: clean numbers (a +10 and -5 per cent pair); percentages with a given price and quantity pair; messier figures with a midpoint calculation; mixed case (find elasticity, name its form, then find the change in revenue)
practice: review: compute three elasticities from new price-quantity pairs and name each form, say which goods have low elasticity and why, compute income and cross elasticity from new data; think: a seller wants more revenue — decide from the elasticity whether to cut or raise the price; pause: after the formula passage and after the revenue passage
sources: yes


=== CH06 ===
title: Consumer Choice: Surplus and Indifference Curves
purpose: Show what a buyer gains from a purchase and how a buyer with a fixed budget picks the best bundle.
pace: slow — first use of indifference curves and a budget line
style: mixed
words: 4575
figures: 4
- fig01: a demand curve with the consumer-surplus triangle shaded
- fig02: a family of indifference curves, convex to the origin
- fig03: a budget line drawn from a spending plan of Tk 1,200
- fig04: the tangency point of curve and budget line marked as the best bundle
plate: a draper's shop with a customer weighing two bolts of cloth against a window, 1880s
sections:
6.1 | Consumption and Consumer Surplus | new idea | 550
6.2 | Indifference Curves and the Budget Line | framework | 775
6.3 | Consumer Equilibrium | technique | 650
concepts:
- 6.1 | consumption and consumer surplus: willingness to pay minus price paid | core | needs: 3.1 utility; 4.2 the law of demand
- 6.2 | indifference curve and its properties | core | needs: 3.1 utility
- 6.2 | budget line | standard | needs: none
- 6.3 | consumer equilibrium where an indifference curve just touches the budget line | core | needs: 6.2 indifference curve; 6.2 budget line
- 6.3 | reading consumer surplus from an indifference diagram | minor | needs: 6.1 consumer surplus
defines:
- Consumption | the using up of goods and services to meet wants
- Willingness to pay | the highest price a buyer would accept to get one unit of a good
- Consumer surplus | the gap between what a buyer would pay and what is actually paid
- Indifference curve | a line joining bundles of two goods that give a consumer the same satisfaction
- Indifference map | a set of indifference curves, with curves farther from the origin showing more satisfaction
- Marginal rate of substitution | the amount of one good a consumer will give up to gain one more unit of the other
- Budget line | a line showing every bundle of two goods a consumer can just afford with a given income
- Consumer equilibrium | the affordable bundle that gives a consumer the greatest satisfaction
assumes: Utility; Marginal utility; Demand curve; Law of demand; Consumer
words-in-use: budget; bundle; surplus
case: Meghna and Sons (illustrative). Consumer surplus: on 14 March 2026 five customers' highest prices for a dictionary were Tk 900, Tk 800, Tk 700, Tk 650 and Tk 600; shelf price Tk 650; four buy and one does not. Surpluses: Tk 250, Tk 150, Tk 50, Tk 0, total Tk 450. Choice: a student's monthly spending plan is Tk 1,200 on prescribed books at Tk 150 each and stationery packs at Tk 100 each. Budget line bundles (books, packs): (0, 12), (2, 9), (4, 6), (6, 3), (8, 0). One indifference curve through (4, 6) also passes through (3, 8) and (6, 4); the slope between (3, 8) and (4, 6) is 2 packs per book, between (4, 6) and (6, 4) it is 1 pack per book. Best bundle: (4, 6), cost Tk 600 plus Tk 600 equals Tk 1,200; the price ratio 150 to 100 equals 1.5 packs per book.
history: Jules Dupuit, 1844, on measuring the usefulness of public works such as bridge tolls; search: Dupuit 1844 utility of public works bridge toll
refs: Chapter 3, 'Utility and Diminishing Marginal Utility', section 3.1 'Utility and Satisfaction' — satisfaction ranked by bundles here; Chapter 4, 'Demand and the Demand Curve', section 4.2 'The Law of Demand' — the curve whose area gives consumer surplus
need: Chapter 3 section 3.1 'Utility and Satisfaction' and Chapter 4 section 4.2 'The Law of Demand'
ladder: familiar case (the dictionary buyers); reshaped case (rice and lentils on a Tk 800 weekly plan); new setting (data and talk time on a phone plan); combined case (a budget change and the new best bundle)
practice: review: compute consumer surplus from a new price list, draw a budget line from new prices, say why indifference curves do not cross; think: a student's income doubles with prices unchanged — describe the new budget line and the likely best bundle; pause: after the first indifference curve is drawn and after the tangency passage
sources: yes


=== CH07 ===
title: Supply and Elasticity of Supply
purpose: Build the supply idea from a price table to a curve and measure how strongly sellers respond to price.
pace: standard — mirrors the demand chapters, so the pace can rise
style: mixed
words: 4700
figures: 4
- fig01: a supply curve drawn from the printer's schedule
- fig02: a shift of the supply curve with its causes labelled
- fig03: a supply curve of labour that bends backward at high pay
- fig04: three supply curves of different elasticity through the same point
plate: a harbour quay with sacks and crates being loaded onto a steamer, 1880s
sections:
7.1 | The Law of Supply | defining theory | 550
7.2 | What Moves the Supply Curve | new idea | 550
7.3 | Exceptions to the Law | framework | 225
7.4 | Elasticity of Supply | technique | 775
concepts:
- 7.1 | supply, the supply schedule and curve, and the law of supply | core | needs: 4.2 the law of demand
- 7.2 | determinants of supply; movement along the curve versus a shift | core | needs: 7.1 law of supply
- 7.3 | exceptional supply curves: fixed supply and the backward-bending curve | standard | needs: 7.1 law of supply
- 7.4 | price elasticity of supply and how to measure it | core | needs: 5.1 price elasticity of demand; 7.1 law of supply
- 7.4 | elastic and inelastic supply, and what sets the size | standard | needs: 7.4 price elasticity of supply
defines:
- Supply | the quantity of a good sellers are willing and able to offer at each possible price, in a given period
- Quantity supplied | the amount sellers plan to offer at one particular price
- Supply schedule | a table listing the quantity supplied at each of several prices
- Supply curve | a line on a graph showing the quantity supplied at each price, other things equal
- Law of supply | when the price of a good rises, quantity supplied rises, and when it falls, quantity supplied falls, other things equal
- Determinants of supply | the things other than the good's own price that change how much sellers offer
- Backward-bending supply curve | a curve showing that beyond some pay level a worker offers fewer hours as pay rises further
- Price elasticity of supply | the percentage change in quantity supplied divided by the percentage change in price
- Elastic supply | supply for which quantity responds by a larger percentage than price
- Inelastic supply | supply for which quantity responds by a smaller percentage than price
assumes: Demand; Demand curve; Law of demand; Percentage change; Price elasticity of demand; Ceteris paribus
words-in-use: supply; curve; offer
case: Meghna and Sons (illustrative). A local printer supplies 200-page exercise books to the shop at a wholesale price. Weekly quantity offered, 9 March 2026: Tk 40, 150 books; Tk 45, 200; Tk 50, 250; Tk 55, 300; Tk 60, 350. Elasticity from Tk 50 to Tk 55: +10 per cent price, +20 per cent quantity, elasticity 2.0 (elastic). Shift: on 1 April 2026 the printer's paper cost rose and it offered 50 fewer books at every price: 100, 150, 200, 250, 300. Exceptional curve 1: a rare first edition, only one copy exists, supply unchanged at any price. Exceptional curve 2: a part-time binder offers 20 hours a week at Tk 150 an hour, 26 hours at Tk 200, 24 hours at Tk 260.
history: The Lancashire cotton famine of 1861 to 1865 and the rise of cotton exports from Egypt and India; search: Lancashire cotton famine 1861 Egypt India cotton exports
refs: Chapter 4, 'Demand and the Demand Curve', section 4.3 'What Moves the Demand Curve' — the same movement-versus-shift logic; Chapter 5, 'Elasticity of Demand', section 5.1 'Measuring Responsiveness' — the percentage method reused
need: Chapter 4 section 4.3 'What Moves the Demand Curve' and Chapter 5 section 5.1 'Measuring Responsiveness'
ladder: familiar case (the printer's schedule); reshaped case (a bakery's tray output); new setting (a fisher's catch before and after the monsoon); combined case (a schedule, a shift and an elasticity in one problem)
practice: review: draw a supply curve from a new schedule, separate five events into movements and shifts, compute and name three elasticities of supply from new data; think: explain why a farmer's supply of a perishable crop is inelastic in the short run; pause: after the shift passage and after the elasticity-of-supply formula
sources: no


=== CH08 ===
title: How Markets Find a Price
purpose: Bring demand and supply together to find a price, show why a market is pulled toward it, and measure who gains.
pace: standard — combines two earlier curves
style: mixed
words: 4600
figures: 4
- fig01: demand and supply curves crossing at the equilibrium point
- fig02: a ceiling below and a floor above equilibrium with the shortage and surplus gaps marked
- fig03: two panels: a supply shift left and a demand shift right with the new equilibria
- fig04: consumer surplus and producer surplus shaded on one diagram
plate: a corn exchange floor with traders around a chalk price board, 1880s
sections:
8.1 | Markets and Market Equilibrium | framework | 550
8.2 | Forces Toward Equilibrium | new idea | 550
8.3 | Shifts and New Equilibria | technique | 450
8.4 | Consumer and Producer Surplus in Practice | new idea | 450
concepts:
- 8.1 | equilibrium price and quantity where demand meets supply | core | needs: 4.2 the law of demand; 7.1 law of supply
- 8.2 | excess demand, excess supply, price ceilings and price floors | core | needs: 8.1 equilibrium
- 8.3 | a shift of demand and the new equilibrium | standard | needs: 4.3 what moves the demand curve; 8.1 equilibrium
- 8.3 | a shift of supply and the new equilibrium | standard | needs: 7.2 what moves the supply curve; 8.1 equilibrium
- 8.4 | producer surplus and total surplus | standard | needs: 6.1 consumer surplus; 8.1 equilibrium
- 8.4 | practical uses of consumer surplus and producer surplus | standard | needs: 8.4 producer surplus
defines:
- Equilibrium | a state in which nothing pushes the price or quantity to change
- Equilibrium price | the price at which quantity demanded equals quantity supplied
- Equilibrium quantity | the quantity bought and sold at the equilibrium price
- Excess demand | the amount by which quantity demanded exceeds quantity supplied at a price below equilibrium
- Excess supply | the amount by which quantity supplied exceeds quantity demanded at a price above equilibrium
- Price ceiling | a legal maximum price that may be charged for a good
- Price floor | a legal minimum price that may be charged for a good
- Producer surplus | the gap between the price a seller receives and the lowest price the seller would accept
- Total surplus | consumer surplus plus producer surplus, a measure of the gain from trade
assumes: Demand curve; Supply curve; Market; Consumer surplus; Determinants of demand; Determinants of supply; Substitute goods
words-in-use: price; surplus; market
case: Meghna and Sons (illustrative). Neighbourhood market for 200-page exercise books, weekly: demand Qd = 1,800 - 15P and supply Qs = 25P - 600, with P in taka. Equilibrium: P = Tk 60, Q = 900. Ceiling at Tk 50: Qd 1,050, Qs 650, excess demand 400. Floor at Tk 70: Qd 750, Qs 1,150, excess supply 400. Supply shift: paper cost rises, supply becomes Qs = 25P - 760; new equilibrium P = Tk 64, Q = 840. Demand intercept price is Tk 120; supply intercept price is Tk 24 before the shift. Consumer surplus at equilibrium: 0.5 x (120 - 60) x 900 = Tk 27,000 a week; producer surplus: 0.5 x (60 - 24) x 900 = Tk 16,200 a week. After the shift: consumer surplus 0.5 x (120 - 64) x 840 = Tk 23,520; producer surplus 0.5 x (64 - 30.4) x 840 = Tk 14,112. Substitute-goods link: when the price of petrol rises, demand for natural gas shifts right (kept as a general example, not shop data).
history: Diocletian's Edict on Maximum Prices, AD 301; search: Diocletian Edict on Maximum Prices 301 shortages
refs: Chapter 4, 'Demand and the Demand Curve', section 4.3 'What Moves the Demand Curve' — causes of a demand shift; Chapter 7, 'Supply and Elasticity of Supply', section 7.2 'What Moves the Supply Curve' — causes of a supply shift; Chapter 6, 'Consumer Choice: Surplus and Indifference Curves', section 6.1 'Consumption and Consumer Surplus' — the surplus idea extended to sellers
need: Chapter 4 section 4.3, Chapter 7 section 7.2 and Chapter 6 section 6.1
ladder: familiar case (the neighbourhood exercise-book market); reshaped case (a fish market at dawn); new setting (a flat-rent market with a legal ceiling); combined case (a shift plus a ceiling plus a change in total surplus)
practice: review: find equilibrium from new equations, describe the adjustment from a price above or below it, trace the effect of a shift; think: a government sets a price ceiling below equilibrium for a staple — describe who gains and who loses; pause: after the equilibrium solution and after the shortage-and-surplus passage
sources: no


=== CH09 ===
title: Production
purpose: Explain how inputs become output, why adding one input yields less and less, and what changes when all inputs grow.
pace: standard — numeric tables, with the reasoning kept in plain words
style: mixed
words: 4700
figures: 4
- fig01: a total product curve rising then flattening and a marginal product curve peaking then falling
- fig02: average and marginal product on one diagram showing where they meet
- fig03: a time bar marking the short run and the long run
- fig04: three paths of output as scale doubles: more than double, double, less than double
plate: a pin-making workshop with a row of workers at benches, 1880s
sections:
9.1 | The Production Function | new idea | 650
9.2 | Short Run and Long Run | framework | 225
9.3 | Diminishing Returns | defining theory | 775
9.4 | Returns to Scale | technique | 450
concepts:
- 9.1 | production function linking inputs to output | core | needs: 1.1 factors of production
- 9.1 | production, input and output as working words | minor | needs: none
- 9.2 | short run with a fixed input, long run with every input variable | standard | needs: 9.1 production function
- 9.3 | the law of diminishing returns | core | needs: 9.2 short run
- 9.3 | total, average and marginal product | standard | needs: 9.1 production function
- 9.4 | increasing, constant and decreasing returns to scale | standard | needs: 9.2 long run
- 9.4 | reading the type from an output table | standard | needs: 9.4 returns to scale
defines:
- Production | the process of turning resources into goods and services
- Input | a resource used in production
- Output | the goods or services produced
- Production function | a rule or table linking the quantities of inputs used to the greatest output they can make
- Short run | a period too short to change at least one input, such as machines or floor space
- Long run | a period long enough to change every input
- Fixed input | an input whose quantity cannot be changed in the short run
- Variable input | an input whose quantity can be changed even in the short run
- Total product | the whole output from a given amount of inputs
- Average product | total product divided by the number of units of the variable input
- Marginal product | the extra output from adding one more unit of the variable input
- Law of diminishing returns | when more of one input is added to fixed inputs, the extra output eventually falls
- Returns to scale | the change in output when all inputs are changed by the same proportion
- Increasing returns to scale | output rises by a larger proportion than inputs
- Constant returns to scale | output rises by the same proportion as inputs
- Decreasing returns to scale | output rises by a smaller proportion than inputs
assumes: Resource; Factor of production; Firm; Marginal utility; Law of diminishing marginal utility
words-in-use: fixed; scale; margin
case: Meghna and Sons (illustrative). On 3 March 2026 the shop opened a binding corner for theses with one binding machine. Short run, one machine and 1 to 6 workers, binds a day: 10, 24, 36, 44, 48, 48. Marginal product: 10, 14, 12, 8, 4, 0. Average product: 10, 12, 12, 11, 9.6, 8. Long run, scale tables (binds a day): one machine and 2 workers, 40; two machines and 4 workers, 90; four machines and 8 workers, 180; eight machines and 16 workers, 300. Types: first doubling gives 2.25 times output (increasing), second doubling gives 2.0 times (constant), third gives about 1.67 times (decreasing).
history: Henry Ford's moving assembly line at Highland Park, 1913, and the fall in chassis assembly time; search: Ford moving assembly line 1913 chassis assembly time hours
refs: Chapter 3, 'Utility and Diminishing Marginal Utility', section 3.2 'The Law of Diminishing Marginal Utility' — the same shape of argument applied to output; Chapter 1, 'Scarcity, Choice and the Economic Problem', section 1.1 'Wants, Resources and Scarcity' — the factors of production
need: Chapter 1 section 1.1 'Wants, Resources and Scarcity' and Chapter 3 section 3.2 'The Law of Diminishing Marginal Utility'
ladder: familiar case (the binding corner's six-worker table); reshaped case (a tailor adding sewing hands to one table); new setting (a rice field adding fertiliser); combined case (a short-run table followed by a long-run scale table)
practice: review: complete average and marginal columns from new data, say where diminishing returns start, classify the returns to scale in a new table; think: explain why a factory cannot simply add workers forever to raise output; pause: after the short-run versus long-run passage and after the marginal-product table
sources: no


=== CH10 ===
title: Costs of Production
purpose: Show what costs a firm counts, how they change with output, and how to reach a given output at the lowest cost.
pace: standard — table work, with each curve explained in plain words
style: mixed
words: 4600
figures: 4
- fig01: fixed, variable and total cost curves on one diagram
- fig02: average cost and marginal cost curves, with marginal cost cutting average cost at its lowest point
- fig03: three short-run average cost curves with the long-run curve enveloping them
- fig04: an isocost line touching an isoquant at the least-cost point
plate: a foundry floor with a tilting converter and ladles of molten metal, 1880s
sections:
10.1 | Cost Concepts | framework | 450
10.2 | Short-Run Cost Curves | technique | 775
10.3 | Long-Run Cost Curves | new idea | 225
10.4 | Least-Cost Combination | technique | 550
concepts:
- 10.1 | explicit and implicit cost, and how opportunity cost is measured | standard | needs: 1.2 opportunity cost
- 10.1 | fixed, variable and total cost; prime and supplementary cost | standard | needs: 9.2 short run; 9.1 production function
- 10.2 | average cost, marginal cost and how the two relate | core | needs: 10.1 cost concepts; 9.3 marginal product
- 10.2 | how total, variable, fixed, marginal and average cost link | standard | needs: 10.1 cost concepts
- 10.3 | the long-run average cost curve as the lower edge of the short-run curves | standard | needs: 10.2 short-run cost curves; 9.2 long run
- 10.4 | least-cost combination of inputs where each taka buys the same extra output | core | needs: 10.1 cost concepts; 9.3 marginal product
defines:
- Cost | the value of the resources used up in making a good or service
- Explicit cost | a cost paid out in money to others, such as rent or wages
- Implicit cost | the value of resources the owner supplies, such as own time, for which no payment is made
- Fixed cost | a cost that stays the same however much is produced in the short run
- Variable cost | a cost that rises and falls with the amount produced
- Total cost | fixed cost plus variable cost at a given output
- Average cost | total cost divided by the number of units produced
- Marginal cost | the extra cost of producing one more unit
- Prime cost | the direct cost of materials and labour that go into a unit of output
- Supplementary cost | the cost of items apart from prime cost, such as rent and equipment, which remain even when output is nil
- Long-run average cost curve | a curve showing the lowest average cost of each output when every input can be changed
- Isoquant | a curve joining the input combinations that all make the same output
- Isocost line | a line joining the input combinations that all cost the same total
- Least-cost combination | the mix of inputs that makes a given output for the lowest total cost
assumes: Opportunity cost; Production function; Short run; Long run; Fixed input; Variable input; Marginal product; Total product
words-in-use: cost; average; marginal
case: Meghna and Sons (illustrative). Binding corner monthly, 2026. Fixed cost Tk 20,000 (corner rent Tk 12,000 plus machine instalment Tk 8,000). Implicit cost: owners' unpaid time Tk 15,000 a month. Prime cost is materials and labour, equal to variable cost. Output (binds a month) 100, 200, 300, 400, 500, 600, 700 with variable cost Tk 4,000; 7,000; 9,000; 12,000; 17,000; 24,000; 34,000. Total cost Tk 24,000; 27,000; 29,000; 32,000; 37,000; 44,000; 54,000. Average cost Tk 240; 135; 96.67; 80; 74; 73.33; 77.14. Marginal cost per bind between steps: Tk 40; 30; 20; 30; 50; 70; 100 (marginal cost crosses average cost near 600 binds, where average cost is lowest at Tk 73.33). Long run: with one machine lowest average cost Tk 73.33 at 600 binds; with two machines Tk 66 at 1,200; with three machines Tk 70 at 1,800. Least-cost combination for 400 binds a day, wage Tk 600 a day and machine rent Tk 1,200 a day: 10 workers and 5 machines cost Tk 12,000; 16 workers and 3 machines Tk 13,200; 8 workers and 8 machines Tk 14,400; 24 workers and 2 machines Tk 16,800; least cost Tk 12,000, where marginal product of labour is 30 and of a machine 60 (30 over 600 equals 60 over 1,200).
history: Henry Bessemer's converter process, 1856, and the fall in the price of steel; search: Bessemer process 1856 steel price fall per ton
refs: Chapter 1, 'Scarcity, Choice and the Economic Problem', section 1.2 'Choice and Opportunity Cost' — the idea behind implicit cost; Chapter 9, 'Production', section 9.3 'Diminishing Returns' — why marginal cost rises
need: Chapter 1 section 1.2 'Choice and Opportunity Cost' and Chapter 9 section 9.3 'Diminishing Returns'
ladder: familiar case (the binding corner's monthly cost table); reshaped case (a tailor's cost sheet for shirts); new setting (a small farm's cost per sack of rice); combined case (cost table, curve reading and least-cost choice in one problem)
practice: review: complete the cost columns from new data, find where marginal cost crosses average cost, choose the cheapest input mix from three priced options; think: explain why a family business should count its own unpaid time as a cost when judging success; pause: after the average-versus-marginal passage and after the least-cost rule
sources: no


=== CH11 ===
title: Market Structures and the Firm
purpose: Compare how firms behave when they face many rivals, one rival or none, and how each structure sets price and output.
pace: standard — long chapter; sections stand largely alone
style: mixed
words: 4925
figures: 5
- fig01: a table-diagram of the market structures by number of sellers, product type and entry
- fig02: a perfectly competitive firm at the point where marginal cost equals price, with industry beside it
- fig03: a monopolist's demand and marginal revenue curves with the profit rectangle
- fig04: a monopolistic competitor's short-run profit and long-run zero profit side by side
- fig05: a revenue comparison of a price cut for an elastic good and an inelastic good
plate: a market street with one grand emporium among small stalls, 1880s
sections:
11.1 | Types of Market | framework | 225
11.2 | Perfect Competition | new idea | 775
11.3 | Monopoly | new idea | 550
11.4 | Monopolistic Competition | new idea | 550
11.5 | Pricing and the Firm's Goal | framework | 225
concepts:
- 11.1 | market structure and competitive market: the four main kinds | standard | needs: 4.1 market
- 11.2 | equilibrium of the firm and of the industry in the short run under perfect competition | core | needs: 10.2 marginal cost; 11.1 market structure
- 11.2 | perfect competition compared with pure competition | standard | needs: 11.1 market structure
- 11.3 | pure monopoly, bilateral monopoly and how a monopolist sets price | core | needs: 11.1 market structure; 10.2 marginal cost
- 11.4 | monopolistic competition and product differentiation, short and long run | core | needs: 11.1 market structure; 10.2 marginal cost
- 11.5 | how structure shapes pricing, why lower pricing is not always good, and whether profit maximisation is always the goal | standard | needs: 5.2 total revenue; 11.2 equilibrium of the firm
defines:
- Market structure | the features of a market, such as number of sellers, type of product and ease of entry, that shape how firms behave
- Competitive market | a market with many buyers and sellers, so no single one can set the price
- Industry | all the firms that make the same or very similar goods
- Price taker | a firm that must accept the market price because it is too small to change it
- Price maker | a firm large enough that its own output choices affect the price
- Marginal revenue | the extra revenue gained by selling one more unit
- Perfect competition | a market with many sellers, an identical product, free entry and full information, so each firm takes the price
- Pure competition | a market with many sellers, an identical product and free entry, where buyers may lack full information or free movement
- Monopoly | a market with one seller and no close substitute, so that seller sets the price
- Pure monopoly | a monopoly in which one seller supplies the whole market with a product that has no close substitute
- Bilateral monopoly | a market with a single seller facing a single buyer
- Monopolistic competition | a market with many sellers of similar but not identical goods and free entry
- Product differentiation | making a firm's good different from rivals' in quality, design, brand or service
- Oligopoly | a market with a few large sellers, each aware of the others' actions
- Profit maximisation | choosing the output at which the gap between total revenue and total cost is greatest
assumes: Market; Marginal cost; Average cost; Total revenue; Price elasticity of demand; Elastic demand; Inelastic demand; Equilibrium price; Excess supply
words-in-use: firm; market; competition
case: Meghna and Sons (illustrative). Perfect competition: exercise books, market price Tk 60. Firm marginal cost by daily output: 10 books, Tk 40; 20, Tk 50; 30, Tk 60; 40, Tk 70; 50, Tk 80. Profit-maximising output 30 (marginal cost equals Tk 60). Average cost at 30 books Tk 52; profit (60 - 52) x 30 = Tk 240 a day. Entry of new shops lowers price toward average cost in the long run. Monopoly: sole authorised seller of one foreign reference work. Price and weekly quantity: Tk 1,000, 10 copies; Tk 900, 20; Tk 800, 30; Tk 700, 40. Total revenue Tk 10,000; 18,000; 24,000; 28,000. Marginal revenue between steps Tk 800; 600; 400. Marginal cost constant Tk 500. Profit-maximising output 30 copies at Tk 800; profit (800 - 500) x 30 = Tk 9,000. Monopolistic competition: a mystery novel series differentiated by cover and author; price Tk 400; short run average cost Tk 340 at 50 copies a week; profit Tk 3,000. After two more shops enter, the shop sells 40 copies at Tk 380 with average cost Tk 380; profit nil. Pricing: price cut from Tk 60 to Tk 55 for the exercise book raised weekly sales from 200 to 210; revenue Tk 12,000 fell to Tk 11,550 (inelastic). Market structure ranking for the shop: exercise books near perfect competition; the sole-authorised reference work a monopoly; mystery novels monopolistic competition.
history: The 1911 US Supreme Court decision to break up Standard Oil; search: Standard Oil 1911 Supreme Court dissolution
refs: Chapter 10, 'Costs of Production', section 10.2 'Short-Run Cost Curves' — marginal cost used to find output; Chapter 5, 'Elasticity of Demand', section 5.2 'Forms of Price Elasticity' — why a price cut can lower revenue; Chapter 8, 'How Markets Find a Price', section 8.2 'Forces Toward Equilibrium' — price taking and adjustment
need: Chapter 10 section 10.2, Chapter 5 section 5.2 and Chapter 8 section 8.2
ladder: familiar case (the exercise-book firm at Tk 60); reshaped case (a sweet-shop in a busy bazaar); new setting (a ride-hailing app with few rivals); combined case (identify the structure from facts, then find the firm's output and profit)
practice: review: find the profit-maximising output from a new cost table in each of three structures, name the structure from a list of features, decide whether a price cut helps revenue; think: assess the view that firms always aim to maximise profit; pause: after the price-taker passage and after the monopoly marginal-revenue table
sources: no


=== CH12 ===
title: Distribution: Rent, Wages, Interest and Profit
purpose: Explain how the money earned from production is shared among land, labour, capital and enterprise.
pace: standard — mostly descriptive, with short worked cases
style: descriptive
words: 4600
figures: 4
- fig01: differential rent on three plots of different yield
- fig02: a labour market with demand and supply setting the wage
- fig03: a loanable-funds diagram setting the rate of interest
- fig04: a stacked bar splitting the shop's yearly sales into costs, normal profit and economic profit
plate: a rent-day gathering in a manor estate office with a steward and tenant farmers, 1880s
sections:
12.1 | Rent | defining theory | 225
12.2 | Wages | framework | 775
12.3 | Interest | framework | 225
12.4 | Profit | framework | 775
concepts:
- 12.1 | economic rent, the Ricardian view of differential rent, and the idea of a differential surplus; factor price and distribution | standard | needs: 8.1 equilibrium; 1.1 factors of production
- 12.2 | how wages are determined by demand for and supply of labour | core | needs: 8.1 equilibrium; 12.1 factor price
- 12.2 | nominal and real wages, and why wages vary | standard | needs: 12.2 wage determination
- 12.3 | how the rate of interest is set by the demand for and supply of loanable funds | standard | needs: 8.1 equilibrium
- 12.4 | risk bearing and marginal productivity theories of profit | core | needs: 12.1 factor price; 12.2 wage determination
- 12.4 | economic profit versus accounting profit, and normal profit | standard | needs: 10.1 explicit cost; 10.1 implicit cost
defines:
- Factor price | the payment a factor of production earns: rent for land, wages for labour, interest for capital, profit for enterprise
- Economic rent | the payment to a factor above the minimum needed to keep it in its present use
- Differential rent | the extra return a better plot earns over the poorest plot in use
- Wage | the payment made to labour for its work
- Nominal wage | the wage counted in money
- Real wage | the amount of goods and services a nominal wage can buy
- Interest | the payment for the use of borrowed money or capital over time
- Rate of interest | the interest paid in a year as a percentage of the amount borrowed
- Profit | the reward of enterprise: what remains of revenue after the other factors are paid
- Economic profit | revenue less all costs, explicit and implicit
- Accounting profit | revenue less explicit costs only
- Normal profit | the least profit that keeps a firm in business, equal to the implicit costs of the owner's own resources
- Risk bearing | taking on the chance of loss when production is uncertain
- Marginal productivity theory | the view that each factor is paid in line with the extra output its last unit adds
assumes: Factor of production; Equilibrium; Equilibrium price; Demand; Supply; Marginal product; Explicit cost; Implicit cost; Total revenue
words-in-use: rent; wage; capital
case: Meghna and Sons (illustrative). Rent: three locations for a stall, yearly figures before rent: main road Tk 150,000; side lane Tk 90,000; marginal plot Tk 60,000 (pays no rent). Differential rent: Tk 90,000; Tk 30,000; nil. The shop itself pays Tk 60,000 a month in rent (carried base fact). Wages: shop assistant's nominal wage Tk 18,000 a month; general prices rose 8 per cent in the year; real wage about Tk 16,667 in last year's prices. Interest: a loan of Tk 200,000 at 11 per cent a year costs Tk 22,000 a year. Profit: yearly sales Tk 6,000,000; explicit costs Tk 5,400,000; accounting profit Tk 600,000. Implicit costs: owners' unpaid time Tk 360,000 and return on their own capital Tk 90,000, total Tk 450,000. Economic profit Tk 150,000; normal profit Tk 450,000.
history: David Ricardo's rent theory in his 1815 essay and his 1817 Principles, and the Corn Laws repealed in 1846; search: Ricardo rent Corn Laws 1815 repeal 1846
refs: Chapter 8, 'How Markets Find a Price', section 8.1 'Markets and Market Equilibrium' — demand and supply applied to factors; Chapter 10, 'Costs of Production', section 10.1 'Cost Concepts' — explicit and implicit cost behind profit
need: Chapter 8 section 8.1 'Markets and Market Equilibrium' and Chapter 10 section 10.1 'Cost Concepts'
ladder: familiar case (the shop's stalls, assistant, loan and ledger); reshaped case (a tea garden's plots, pickers and lender); new setting (a coastal shrimp farm); combined case (all four payments in one business's yearly account)
practice: review: compute differential rents for new plots, compute a real wage from new price data, separate economic profit from accounting profit in a new account; think: explain why the poorest plot in use earns no rent; pause: after the differential-rent passage and after the economic-versus-accounting profit passage
sources: yes


=== A1 ===
title: Maths You Will Use
purpose: Give a one-to-two-page reference for the arithmetic the calculation chapters rely on.
pace: standard — reference, not a lesson
style: calculation
words: 1000
figures: 1
- fig01: a number line and a small graph showing how to read a straight line from two points
sections:
A1.1 | Percentages and percentage change | technique | 250
A1.2 | Ratios, averages and rounding | technique | 250
A1.3 | Rearranging an equation | technique | 250
A1.4 | Reading a graph | technique | 250
concepts:
- A1.1 | percentage and percentage change, with a worked taka example | standard | needs: none
- A1.2 | ratio, average and rounding to a stated number of places | standard | needs: none
- A1.3 | rearranging a linear equation such as Q = 1,800 - 15P to find P | standard | needs: none
- A1.4 | reading values, slope and intercepts from a straight-line graph | standard | needs: none
defines: none (reference only; terms stay with the chapters that own them)
assumes: none
words-in-use: none
case: none
history: none
refs: Chapter 5, 'Elasticity of Demand', section 5.1 'Measuring Responsiveness' — percentage change in use; Chapter 8, 'How Markets Find a Price', section 8.1 'Markets and Market Equilibrium' — equations solved
need: nothing
ladder: clean numbers first (a Tk 60 price rising by 10 per cent), then messier numbers (a rise from Tk 62 to Tk 67), then an equation to rearrange, then a graph to read
practice: review: two percentage changes, one average and one rearrangement from new data; think: none; pause: none
sources: no
