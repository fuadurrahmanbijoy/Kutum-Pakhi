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
course: MGT 105
book: Principles of Finance
spelling: British · dates: day, month, year (12 March 2026) · country: mixed, no single country; the running case is in Bangladesh; name the place whenever law or standards differ · currency and numbers: taka for the running case, written Tk 158,000 (international digit grouping); a historical case keeps its own currency
running case: Meghna and Sons — illustrative. Base facts (FIXED): a family bookshop in Dhaka, founded 12 March 2011 by Meghna Chowdhury as a sole proprietorship, a partnership with her sons Rafi and Tanvir (equal thirds) from 1 July 2018; financial year 1 July to 30 June; year to 30 June 2025: sales Tk 4,200,000, profit Tk 320,000; assumed tax rate 25% for illustration
chosen words (one term, one word):
- use finance — also called corporate finance, financial management
- use financial manager — also called finance manager, chief financial officer
- use shareholder — also called stockholder, equity holder
- use common stock — also called ordinary shares, equity shares
- use preferred stock — also called preference shares
- use face value — also called par value, principal of a bond
- use principal — the owner who hires an agent; the starting sum of money is the principal sum
- use coupon rate — also called coupon interest rate
- use required return — also called required rate of return
- use payback period — also called PBP
- use net present value — also called NPV
- use yield to maturity — also called YTM
- use company — also called corporation, limited company
- use cash conversion cycle — also called net operating cycle
size plan: 16 chapters and one appendix, ~67750 words, ~281 pages
chapters:
1. What Finance Is
2. The Financial Manager's Decisions
3. The Goal of the Firm and Agency Theory
4. Interest and Future Value
5. Present Value and Discounting
6. Annuities
7. Capital Budgeting: Process and Cash Flows
8. Evaluating Projects: Payback and Net Present Value
9. Risk and Return
10. Leverage
11. Required Return, CAPM and Market Efficiency
12. Valuation of Bonds
13. Valuation of Shares
14. Working Capital and Short-Term Financing
15. Long-Term Financing and the Capital Market
16. Leasing
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
title: What Finance Is
purpose: Show what finance is, how it differs from its neighbours, and where it sits inside a business.
pace: slow — every term is new and the chapter also teaches the reader how to use the book
style: descriptive
words: 4225
figures: 1
- fig01: the flow of money between a firm, its owners, its lenders and the markets
plate: a merchant's counting-house with coin chests, scales and a clerk at a high desk, 1860s
sections:
1.1 | Finance in plain words | new idea | 650
1.2 | Finance beside its neighbouring subjects | framework | 325
1.3 | The finance function inside a firm | framework | 650
concepts:
- 1.1 | finance | core | needs: none
- 1.1 | cash flow | minor | needs: finance
- 1.2 | finance as a discipline | standard | needs: finance
- 1.2 | finance and management | minor | needs: finance as a discipline
- 1.3 | forms of business | minor | needs: none
- 1.3 | role of finance in a firm | core | needs: forms of business
defines:
- Finance | The activity of finding money, using it, and judging whether the result was worth it. A shop owner who borrows to buy stock does finance.
- Cash flow | Money that actually moves into or out of a business. Paying a supplier Tk 5,000 is a cash flow of minus Tk 5,000.
- Profit | What a business earns from sales after subtracting the costs of earning them. Sales of Tk 100 and costs of Tk 80 leave profit of Tk 20.
- Operating efficiency | How much useful output a business gets from the money and effort it uses. A shop that sells more per taka of stock is more efficient.
- Sole proprietorship | A business owned and run by one person, who keeps all profit and answers for all debts.
- Partnership | A business owned by two or more people who agree to run it together and share its profit.
- Company | A business set up as a legal person of its own, owned through shares, so the owners are separate from the business.
assumes: none
words-in-use: Value; Capital
case: Case file, illustrative. Meghna and Sons is a family bookshop in Dhaka, founded on 12 March 2011 by Meghna Chowdhury as a sole proprietorship and turned into a partnership with her sons Rafi and Tanvir (equal one-third shares) on 1 July 2018. Year 1 July 2024 to 30 June 2025: sales Tk 4,200,000; cost of books sold Tk 2,730,000; other operating expenses Tk 1,150,000; profit Tk 320,000 (4,200,000 - 2,730,000 - 1,150,000). Invoices to schools unpaid at 30 June 2025: Tk 250,000. Cash held 1 July 2024: Tk 110,000; 30 June 2025: Tk 180,000, so cash rose by Tk 70,000 (320,000 - 250,000). Lesson: profit of Tk 320,000 but cash up only Tk 70,000, because Tk 250,000 of sales is not yet collected.
history: The Dutch East India Company (VOC), chartered 1602, sold shares to the public that traded in Amsterdam, an early company separating owners from managers. Search: VOC 1602 first shares Amsterdam exchange.
refs: Chapter 2, 'The Financial Manager's Decisions', section 2.1 'The three big decisions' — turns the idea of finance into three decisions; Chapter 3, 'The Goal of the Firm and Agency Theory', section 3.3 'Owners, managers and agency theory' — returns to owners and managers.
need: nothing
ladder: 1 a household budget (familiar case: pocket money, saving, borrowing); 2 a market stall with credit sales (reshaped case); 3 a small workshop choosing between partnership and company (new setting); 4 a bookshop whose profit and cash disagree, combining profit, cash flow and business form
practice: review: say in plain words what finance covers and how it differs from accounting and from management; tell profit from cash flow using a new set of sales and collection figures; compare sole proprietorship, partnership and company for a new tailoring shop; think: a printing press shows a good profit yet cannot pay wages — find the cause and name the finance issue; pause: after the finance definition, after profit versus cash flow
sources: no

=== CH02 ===
title: The Financial Manager's Decisions
purpose: Name the three decisions every business makes with money and describe the financial manager who makes or guides them.
pace: slow — many new terms close together; the balance sheet is a new way of looking at a business
style: descriptive
words: 3925
figures: 1
- fig01: a balance sheet drawn with the three decisions marked on it
plate: a banker at a high desk reviewing a ledger by gaslight, 1880s
sections:
2.1 | The three big decisions | framework | 550
2.2 | What a financial manager does | framework | 550
2.3 | Decisions on the balance sheet | new idea | 225
concepts:
- 2.1 | investment decision | standard | needs: balance-sheet view of the firm
- 2.1 | financing decision | standard | needs: investment decision
- 2.1 | dividend decision | minor | needs: financing decision
- 2.2 | functions of the financial manager | standard | needs: investment decision
- 2.2 | organisation of the finance function | minor | needs: functions of the financial manager
- 2.2 | financial planning and control | standard | needs: functions of the financial manager
- 2.3 | balance-sheet view of the firm | standard | needs: role of finance in a firm (Chapter 1)
defines:
- Financial manager | The person who decides how a business finds, uses and protects its money. In a small shop this may be the owner.
- Investment decision | A choice about which assets to buy, such as stock, a van or a new shop, in order to earn more money.
- Financing decision | A choice about where the money comes from: owners' own funds, a loan, or new owners.
- Dividend | A share of a company's profit paid out to its owners instead of being kept in the business.
- Dividend decision | A choice about how much profit to pay out to owners and how much to keep for the business.
- Treasurer | The officer in charge of handling cash, raising money and keeping relations with banks.
- Controller | The officer in charge of accounting records, reports and checking that money is used as planned.
- Financial planning | Estimating the money a business will need and receive in future, and arranging how to meet the gap.
- Balance sheet | A statement listing what a business owns and what it owes on one date.
- Asset | Something a business owns that has value, such as cash, stock or a van.
- Liability | Money a business owes to others, such as a bank loan or an unpaid supplier bill.
- Equity | What is left for the owners when liabilities are subtracted from assets.
assumes: finance; cash flow; profit; company; partnership; sole proprietorship
words-in-use: Balance; Stock
case: Case file, illustrative. Meghna and Sons balance sheet at 30 June 2025. Assets: cash Tk 180,000; school invoices owed to the shop Tk 250,000; stock of books Tk 1,350,000; shop fittings Tk 620,000; total Tk 2,400,000. Liabilities: unpaid supplier bills Tk 430,000; bank loan Tk 600,000 (interest 10% a year); total Tk 1,030,000. Equity Tk 1,370,000 (2,400,000 - 1,030,000). Decisions of the year: investment — storage room being considered at Tk 400,000; financing — bank loan of Tk 600,000 taken earlier; dividend — the partners withdrew Tk 120,000 of the Tk 320,000 profit, so Tk 200,000 stayed in the business.
history: General Motors in the 1920s: Donaldson Brown, who had come from DuPont, built financial controls linking return on investment to decisions. Search: Donaldson Brown General Motors DuPont financial control 1920s.
refs: Chapter 1, 'What Finance Is', section 1.3 'The finance function inside a firm' — the function that these decisions fill; Chapter 7, 'Capital Budgeting: Process and Cash Flows', section 7.1 'Why firms budget for capital' — the investment decision in detail.
need: Chapter 1, 'What Finance Is': sections 1.1 'Finance in plain words' and 1.3 'The finance function inside a firm'
ladder: 1 a family kitchen deciding what to buy, how to pay and what to save (familiar case); 2 a tea stall owner adding a second stall (reshaped case); 3 a small garment company in another country (new setting); 4 a bookshop whose balance sheet shows all three decisions at once, combining Chapter 1 ideas
practice: review: name and tell apart the three decisions using a new business; state the work of a treasurer and a controller; build a balance sheet from a new list of items and check that it balances; think: a pharmacy owner has Tk 300,000 of spare cash and three uses for it — sort the uses into the three decisions; pause: after the three decisions, after the balance sheet
sources: no

=== CH03 ===
title: The Goal of the Firm and Agency Theory
purpose: Explain why wealth, not profit alone, is the goal of financial management, and what happens when managers and owners want different things.
pace: slow — abstract ideas (wealth, agency) with several moving parts
style: descriptive
words: 4250
figures: 1
- fig01: the owner-and-manager relationship with the points where interests can differ
plate: a company boardroom table with directors, quill pens and a bound minute book, 1870s
sections:
3.1 | Profit maximisation and its limits | framework | 225
3.2 | Wealth maximisation | new idea | 650
3.3 | Owners, managers and agency theory | defining theory | 775
concepts:
- 3.1 | profit maximisation | standard | needs: profit (Chapter 1)
- 3.2 | wealth maximisation | core | needs: profit maximisation
- 3.2 | stakeholders and social responsibility | minor | needs: wealth maximisation
- 3.3 | agency relationship | core | needs: wealth maximisation
- 3.3 | agency problems, costs and remedies | standard | needs: agency relationship
defines:
- Profit maximisation | Aiming to make the largest profit possible, usually within one year.
- Wealth maximisation | Aiming to raise the value of the owners' investment over time, taking account of when money arrives and how risky it is.
- Shareholder | A person who owns part of a company by holding its shares.
- Share price | The price at which one share of a company can be bought or sold today.
- Stakeholder | Anyone affected by a firm's actions, such as staff, customers, lenders and the community.
- Principal | A person who hires another to act for them. A shop owner who hires a manager is a principal.
- Agent | A person who acts for a principal and makes decisions for the principal. A hired shop manager is an agent.
- Agency problem | A conflict that arises when an agent's own interests differ from those of the principal.
- Agency cost | A cost the principal bears to reduce the agency problem or from the loss it still causes.
- Incentive | A reward, such as a bonus, that encourages a person to act in a chosen way.
assumes: finance; profit; company; partnership; dividend; financial manager; investment decision
words-in-use: Share; Agent
case: Case file, illustrative. Decision dated 15 July 2025: the partners compare two three-year plans for Meghna and Sons. Plan A (deep discounts): profit Tk 380,000, 300,000 and 250,000 in years 1 to 3 (total Tk 930,000); year-1 sales Tk 4,900,000. Plan B (build school accounts): profit Tk 320,000, 340,000 and 360,000 (total Tk 1,020,000); year-1 sales Tk 4,400,000. A hired manager, Nasir Ahmed, is offered Tk 45,000 a month from 1 September 2025. Bonus rule 1: 1% of sales. Under rule 1 his bonus in year 1 is Tk 49,000 (Plan A) or Tk 44,000 (Plan B). Bonus rule 2: 5% of three-year total profit, giving Tk 46,500 (Plan A) or Tk 51,000 (Plan B). Rule 1 rewards the plan the partners prefer less; rule 2 rewards the plan they prefer.
history: Berle and Means, The Modern Corporation and Private Property (1932), and Jensen and Meckling (1976) on agency costs. Search: Jensen Meckling 1976 theory of the firm agency costs.
refs: Chapter 1, 'What Finance Is', section 1.1 'Finance in plain words' — profit as defined there; Chapter 5, 'Present Value and Discounting', section 5.1 'Discounting a single sum' — how timing is measured in wealth.
need: Chapter 1, 'What Finance Is': section 1.1 'Finance in plain words'; Chapter 2, 'The Financial Manager's Decisions': section 2.1 'The three big decisions'
ladder: 1 a student choosing between a summer job and a course (familiar case: now versus later); 2 a market trader choosing between a quick sale and a loyal customer (reshaped case); 3 a listed company whose chief executive gets a bonus on sales (new setting); 4 a bookshop where plan choice, manager bonus and owners' wealth interact, combining Chapters 1 and 2
practice: review: explain why the aim of the largest profit can mislead, using new yearly figures; define wealth maximisation and say how it differs from profit maximisation; describe an agency problem and two remedies in a hospital-equipment firm; think: a manager is paid on sales and the owners want lasting value — redesign the bonus; pause: after profit maximisation, after the agency relationship
sources: yes

=== CH04 ===
title: Interest and Future Value
purpose: Teach why money changes in value over time and how to find the future value of a sum under simple and compound interest.
pace: slow — the time value of money is new and abstract; smallest numbers first
style: calculation
words: 4225
figures: 2
- fig01: a timeline for a three-year deposit
- fig02: simple interest and compound interest growth of Tk 100,000 over ten years drawn side by side
plate: an hourglass, a coin purse and an open savings passbook arranged as a still life, 1850s
sections:
4.1 | Why time changes the value of money | new idea | 550
4.2 | Simple and compound interest | new idea | 650
4.3 | Future value of a single sum | technique | 425
concepts:
- 4.1 | time value of money | core | needs: none
- 4.2 | simple interest | minor | needs: time value of money
- 4.2 | compound interest | core | needs: simple interest
- 4.3 | future value of a single sum | standard | needs: compound interest
- 4.3 | timelines | minor | needs: future value of a single sum
- 4.3 | compounding more than once a year | minor | needs: future value of a single sum
defines:
- Time value of money | The idea that a taka received today is worth more than a taka received later.
- Opportunity cost | What you give up by choosing one use of money instead of the best alternative.
- Interest | The payment a borrower makes to a lender for the use of money, or the reward a saver earns.
- Interest rate | The interest for one period written as a percentage of the sum, for example 8% a year.
- Principal sum | The original amount lent, borrowed or deposited, before any interest is added.
- Simple interest | Interest calculated only on the principal sum, so it is the same every period.
- Compound interest | Interest calculated on the principal sum and also on interest already earned.
- Future value | What a sum today will be worth at a later date when it earns interest.
- Compounding period | The length of time after which interest is added to the balance, such as a year or six months.
- Timeline | A line marking each period, with the cash flow written at the point where it occurs.
- Factor table | A table of ready-made multipliers that saves repeating a long calculation.
assumes: finance; cash flow; profit
words-in-use: Interest; Principal; Rate
case: Case file, illustrative. Fixed deposit opened 1 July 2025: Tk 100,000 at 8% a year for three years. Simple interest: Tk 24,000 interest, total Tk 124,000. Compound interest (yearly): total Tk 125,971.20 (100,000 x 1.08 x 1.08 x 1.08). Compounded every six months at 4% per half-year for six periods: Tk 126,531.90. The extra Tk 1,971.20 over simple interest is interest earned on interest.
history: Richard Price, the 1772 Appeal on the National Debt, and the British sinking fund of 1786 that his compound-interest argument helped to inspire. Search: Richard Price sinking fund 1786 compound interest.
refs: Chapter 5, 'Present Value and Discounting', section 5.1 'Discounting a single sum' — reverses this chapter's idea; Chapter 3, 'The Goal of the Firm and Agency Theory', section 3.2 'Wealth maximisation' — why timing matters to wealth.
need: Chapter 1, 'What Finance Is': section 1.1 'Finance in plain words'
ladder: 1 round numbers (Tk 100 at 10% for one year, then two); 2 realistic figures (Tk 100,000 at 8% for three years); 3 find the missing rate or number of years from a stated future value; 4 a deposit compounded twice a year compared with a yearly one, using the Chapter 4 factor table
practice: review: explain why a taka today beats a taka next year, with new figures; compute simple and compound interest on Tk 50,000 at 12% for four years; use a factor table to find a future value for a new rate and period; think: two banks offer the same quoted rate but compound at different intervals — choose; pause: after opportunity cost, after compound interest
sources: no

=== CH05 ===
title: Present Value and Discounting
purpose: Teach how to bring future cash flows back to today's value and how to compare streams of cash flows.
pace: slow — reverses the idea of Chapter 4 and introduces streams of unequal sums
style: calculation
words: 4025
figures: 2
- fig01: a timeline showing a future sum brought back to today year by year
- fig02: present value of one future sum falling as the discount rate rises
plate: a pocket watch and a small balance scale holding a coin against a bag of grain, still life, 1860s
sections:
5.1 | Discounting a single sum | technique | 650
5.2 | Mixed streams of cash flows | technique | 550
5.3 | Comparing streams of cash flows | technique | 225
concepts:
- 5.1 | present value of a single sum | core | needs: future value of a single sum (Chapter 4)
- 5.1 | discount rate | minor | needs: present value of a single sum
- 5.2 | mixed stream | standard | needs: present value of a single sum
- 5.2 | present value of a mixed stream | standard | needs: mixed stream
- 5.2 | future value of a mixed stream | minor | needs: mixed stream
- 5.3 | choosing between streams by present value | standard | needs: present value of a mixed stream
defines:
- Present value | What a sum due in the future is worth today.
- Discounting | Finding present value by removing the interest a sum could earn before it arrives.
- Discount rate | The yearly percentage used in discounting; it states the return you could earn elsewhere.
- Cash inflow | Money coming into a business or to an investor, shown as a positive number.
- Cash outflow | Money going out of a business or from an investor, shown as a negative number.
- Mixed stream | A series of cash flows of different sizes in different periods.
assumes: cash flow; time value of money; interest rate; compound interest; future value; timeline; factor table
words-in-use: Discount; Present
case: Case file, illustrative. (a) A school owes Meghna and Sons Tk 250,000 due in one year; at a discount rate of 10% its present value is Tk 227,272.73. (b) A school group offers two payment plans for a bulk contract, discount rate 10%, payments at the end of years 1, 2 and 3. Plan P: Tk 60,000, 80,000, 100,000; present value Tk 195,792.64; future value at the end of year 3 Tk 260,600. Plan Q: Tk 100,000, 80,000, 60,000; present value Tk 202,103.68; future value Tk 269,000. Both plans total Tk 240,000, but Plan Q is worth more because larger sums arrive earlier.
history: Irving Fisher, The Theory of Interest (1930), which states the discounting idea in its modern form. Search: Irving Fisher Theory of Interest 1930 present value.
refs: Chapter 4, 'Interest and Future Value', section 4.3 'Future value of a single sum' — the reverse step; Chapter 8, 'Evaluating Projects: Payback and Net Present Value', section 8.2 'Net present value' — uses discounting on project cash flows.
need: Chapter 4, 'Interest and Future Value': sections 4.2 'Simple and compound interest' and 4.3 'Future value of a single sum'
ladder: 1 round numbers (Tk 110 due in a year at 10%); 2 realistic figures (Tk 250,000 due in 18 months at 9%); 3 a three-payment stream with unequal sums; 4 two streams compared at two different discount rates, with Chapter 4 future value as a check
practice: review: explain discounting as the reverse of compounding using new figures; find the present value of a single sum for two discount rates; find present value of a mixed stream and compare two streams; think: a buyer offers a lump sum now or three later payments — choose and justify; pause: after present value of a single sum, after the mixed stream
sources: no

=== CH06 ===
title: Annuities
purpose: Teach annuities: equal payments at equal intervals, their future and present values, the due form, and finding the payment needed.
pace: slow — a new family of formulas built on Chapters 4 and 5
style: calculation
words: 4375
figures: 2
- fig01: timelines of an ordinary annuity and an annuity due side by side
- fig02: growth of yearly deposits into a single balance
plate: a clerk counting out regular payments at a post-office window with a queue, 1880s
sections:
6.1 | What an annuity is | new idea | 225
6.2 | Future value of an annuity | technique | 775
6.3 | Present value of an annuity | technique | 550
6.4 | Solving for the payment | technique | 225
concepts:
- 6.1 | annuity and its types | standard | needs: mixed stream (Chapter 5)
- 6.2 | future value of an ordinary annuity | core | needs: annuity and its types
- 6.2 | annuity due | standard | needs: future value of an ordinary annuity
- 6.3 | present value of an ordinary annuity | core | needs: annuity and its types
- 6.4 | required periodic payment | standard | needs: future value of an ordinary annuity
defines:
- Annuity | A series of equal payments made at equal intervals for a fixed number of periods.
- Ordinary annuity | An annuity whose payments fall at the end of each period.
- Annuity due | An annuity whose payments fall at the start of each period.
- Instalment | One of a series of regular payments used to repay a loan or build a sum.
assumes: future value; present value; discounting; discount rate; interest rate; compound interest; timeline; factor table; mixed stream; cash inflow; cash outflow
words-in-use: Due; Payment
case: Case file, illustrative. Storage-room fund, deposits at the end of each year from 30 June 2026 for five years at 8%: Tk 50,000 a year gives Tk 293,330.05 as an ordinary annuity and Tk 316,796.45 if deposits are made at the start of each year (annuity due). To reach Tk 400,000 in five years at 8% with equal end-of-year deposits, the required payment is Tk 68,182.58. A supplier offers an instalment plan of Tk 40,000 a year for four years; at 10% its present value is Tk 126,794.62.
history: Johan de Witt, 1671 report to the States of Holland on valuing life annuities for the Dutch Republic. Search: Johan de Witt 1671 life annuities valuation.
refs: Chapter 4, 'Interest and Future Value', section 4.3 'Future value of a single sum' — each payment grows this way; Chapter 12, 'Valuation of Bonds', section 12.3 'Pricing a bond' — bond interest is an annuity.
need: Chapter 4, 'Interest and Future Value': section 4.3 'Future value of a single sum'; Chapter 5, 'Present Value and Discounting': sections 5.1 'Discounting a single sum' and 5.2 'Mixed streams of cash flows'
ladder: 1 round numbers (Tk 100 a year for three years at 10%, added payment by payment); 2 realistic figures (Tk 50,000 a year for five years at 8%); 3 find the payment for a stated goal, or the loan instalment for a stated loan; 4 an annuity due compared with an ordinary annuity and with a mixed stream from Chapter 5
practice: review: say what makes a series of payments an annuity and name its two timing forms; find the future value of an annuity for several rate and period pairs as ordinary and as due; find the present value of a new instalment plan; compute the yearly deposit needed for a stated goal; think: a saver can deposit at the start or the end of each year — find the gain from the earlier timing; pause: after annuity types, after future value of an ordinary annuity
sources: no

=== CH07 ===
title: Capital Budgeting: Process and Cash Flows
purpose: Explain what capital budgeting is, the steps of the process, and how to find the cash flows that matter for a project.
pace: standard — ideas are new but few, and Chapters 4 to 6 give the tools
style: mixed
words: 4125
figures: 1
- fig01: a timeline of one project's initial, yearly and final cash flows
plate: an engineer unrolling the plans of a railway bridge on a drawing table, 1860s
sections:
7.1 | Why firms budget for capital | new idea | 650
7.2 | The steps of the process | framework | 225
7.3 | Cash flows from an investment | technique | 650
concepts:
- 7.1 | capital budgeting | core | needs: investment decision (Chapter 2)
- 7.1 | kinds of projects | minor | needs: capital budgeting
- 7.2 | steps of capital budgeting | standard | needs: capital budgeting
- 7.3 | relevant cash flows | core | needs: steps of capital budgeting
- 7.3 | initial, operating and terminal cash flows | minor | needs: relevant cash flows
defines:
- Capital budgeting | Planning and choosing long-lasting investments by comparing the money they cost with the money they should bring.
- Capital expenditure | Spending on an asset that will help a business for more than one year.
- Independent project | A project that can be accepted or rejected without affecting any other project.
- Mutually exclusive projects | Projects of which only one can be chosen, because choosing one rules out the other.
- Relevant cash flow | A cash flow that changes because of the decision being studied.
- Sunk cost | Money already spent that cannot be recovered whatever you decide now.
- Initial investment | The cash flows at the start of a project to buy and prepare the asset.
- Operating cash flow | The cash a project brings in each year after paying its cash costs and tax.
- Terminal cash flow | The cash received or paid when a project ends, such as the sale of scrap.
- Depreciation | The share of an asset's cost charged against income each year as the asset wears out.
assumes: investment decision; cash flow; cash inflow; cash outflow; timeline; asset; profit
words-in-use: Project; Budget
case: Case file, illustrative. Meeting of 10 August 2025: Meghna and Sons has Tk 400,000 and one free site, so the partners study two mutually exclusive projects, each costing Tk 400,000. Project A (storage room): building work Tk 340,000 plus shelving Tk 60,000 = initial investment Tk 400,000. A survey fee of Tk 20,000 paid on 5 March 2025 is a sunk cost and is left out. Each year for five years: extra sales Tk 300,000; extra cash costs Tk 140,000; depreciation Tk 80,000 (400,000 over 5 years); taxable income Tk 80,000; tax at an assumed 25% is Tk 20,000; operating cash flow = 160,000 - 20,000 = Tk 140,000. Terminal cash flow: scrap Tk 40,000 at the end of year 5 (tax on it ignored for simplicity). Project B (online ordering) also costs Tk 400,000; its after-tax cash flows, scrap included, are Tk 30,000, 90,000, 180,000, 260,000 and 320,000 in years 1 to 5.
history: The Concorde programme: UK and France agreed in 1962 to build it and continued after costs soared, a famous example of sunk-cost thinking; service ended in 2003. Search: Concorde sunk cost fallacy 1962 treaty cost overrun.
refs: Chapter 2, 'The Financial Manager's Decisions', section 2.1 'The three big decisions' — the investment decision studied here; Chapter 8, 'Evaluating Projects: Payback and Net Present Value', section 8.1 'Payback period' — turns these cash flows into a decision.
need: Chapter 2, 'The Financial Manager's Decisions': section 2.1 'The three big decisions'; Chapter 5, 'Present Value and Discounting': section 5.1 'Discounting a single sum'
ladder: 1 round numbers (a machine for Tk 1,000 that adds Tk 400 a year for three years); 2 realistic figures with depreciation and tax (the storage room); 3 spot which listed items are sunk or irrelevant in a new project; 4 build the full cash-flow list for a new project and link it to the Chapter 5 timeline
practice: review: say why capital budgeting matters to a business, with a new example; list the steps of the process in order and what each step produces; sort a list of costs into relevant and sunk; find the operating cash flow from a new set of sales, costs, depreciation and tax; think: a half-built shop needs Tk 200,000 more — decide using only relevant cash flows; pause: after the steps, after relevant cash flows
sources: no

=== CH08 ===
title: Evaluating Projects: Payback and Net Present Value
purpose: Teach the main tests for judging a project: payback period, net present value, internal rate of return and profitability index, and how to choose among them.
pace: standard — four related tools, each built on Chapters 5 to 7
style: calculation
words: 4125
figures: 2
- fig01: cumulative cash flow of two projects showing where each recovers the investment
- fig02: net present value of two projects at different discount rates
plate: a surveyor with a theodolite beside a canal under construction, 1850s
sections:
8.1 | Payback period | technique | 325
8.2 | Net present value | technique | 650
8.3 | Other measures of a project | technique | 325
8.4 | Choosing among methods | framework | 225
concepts:
- 8.1 | payback period | standard | needs: initial, operating and terminal cash flows (Chapter 7)
- 8.1 | discounted payback | minor | needs: payback period
- 8.2 | net present value | core | needs: present value of a mixed stream (Chapter 5)
- 8.2 | accept, reject and rank | minor | needs: net present value
- 8.3 | internal rate of return | standard | needs: net present value
- 8.3 | profitability index | minor | needs: net present value
- 8.4 | comparing the methods | standard | needs: internal rate of return
defines:
- Payback period | The time a project takes to return its initial investment from its cash flows.
- Discounted payback period | The payback time when each cash flow is first discounted to present value.
- Net present value | The present value of all a project's future cash flows minus its initial investment.
- Internal rate of return | The discount rate at which a project's net present value is exactly zero.
- Profitability index | Present value of future cash flows divided by the initial investment.
assumes: present value; discounting; discount rate; mixed stream; annuity; capital budgeting; mutually exclusive projects; independent project; initial investment; operating cash flow; terminal cash flow
words-in-use: Net
case: Case file, illustrative. Projects A and B from the meeting of 10 August 2025, each with initial investment Tk 400,000, discount rate 12%, mutually exclusive. After-tax cash flows, years 1 to 5. Project A: Tk 140,000, 140,000, 140,000, 140,000, 180,000. Project B: Tk 30,000, 90,000, 180,000, 260,000, 320,000. Payback: A 2.86 years, B 3.38 years. Discounted payback: A 3.72 years, B 4.04 years. Net present value: A Tk 127,365.74, B Tk 173,464.90. Internal rate of return: A 23.77%, B 23.67%. Profitability index: A 1.32, B 1.43. Payback favours A; net present value and profitability index favour B.
history: The Channel Tunnel, opened 6 May 1994, whose traffic forecasts and costs differed greatly from plan. Search: Channel Tunnel 1994 forecast traffic cost overrun Eurotunnel.
refs: Chapter 7, 'Capital Budgeting: Process and Cash Flows', section 7.3 'Cash flows from an investment' — source of the cash flows; Chapter 5, 'Present Value and Discounting', section 5.2 'Mixed streams of cash flows' — the discounting used here.
need: Chapter 5, 'Present Value and Discounting': sections 5.1 'Discounting a single sum' and 5.2 'Mixed streams of cash flows'; Chapter 7, 'Capital Budgeting: Process and Cash Flows': section 7.3 'Cash flows from an investment'
ladder: 1 round numbers (cost Tk 1,000, inflows Tk 500 for three years); 2 realistic uneven flows at a stated rate; 3 two projects that the tests rank differently, and a choice with reasons; 4 a project whose discount rate changes, using Chapter 5 tables
practice: review: compute payback and net present value for new project data and state the decision rule for each; say what the internal rate of return means in plain words; rank three new projects by profitability index; think: tests disagree on two storage proposals — decide and explain which test to trust; pause: after payback, after net present value
sources: no

=== CH09 ===
title: Risk and Return
purpose: Define return and risk, separate business risk from financial risk, and measure risk using a probability distribution, the expected value, the standard deviation and the coefficient of variation.
pace: standard — slow down on standard deviation, the one hard step
style: mixed
words: 4475
figures: 2
- fig01: bar charts of the possible returns of two investments with their probabilities
- fig02: two investments marked on axes of expected return and risk
plate: a lighthouse on a rocky coast with a sailing ship in a rough sea, 1860s
sections:
9.1 | Return and risk | new idea | 650
9.2 | Describing uncertainty | technique | 450
9.3 | Measuring risk | technique | 775
concepts:
- 9.1 | rate of return | standard | needs: none
- 9.1 | risk | standard | needs: rate of return
- 9.1 | business risk | minor | needs: risk
- 9.1 | financial risk | minor | needs: business risk
- 9.2 | probability distribution | standard | needs: risk
- 9.2 | expected value | standard | needs: probability distribution
- 9.3 | standard deviation | core | needs: expected value
- 9.3 | coefficient of variation | standard | needs: standard deviation
defines:
- Return | The gain or loss from an investment, including income received and any change in value.
- Rate of return | The return in one period divided by the sum invested, written as a percentage.
- Risk | The chance that the actual result will differ from the result you expect.
- Business risk | Risk that comes from the firm's own trade, such as falling sales or rising costs, before any borrowing.
- Financial risk | Extra risk that comes from borrowing, because interest must be paid whatever the sales.
- Probability distribution | A list of possible results with the chance of each, the chances adding to one.
- Expected value | The average of possible results, each weighted by its probability.
- Variance | The probability-weighted average of the squared gaps between each result and the expected value.
- Standard deviation | The square root of the variance; it shows how far results typically stray from the expected value.
- Coefficient of variation | Standard deviation divided by expected value, giving risk per unit of expected return.
assumes: finance; profit; cash flow; interest rate; asset; liability; time value of money
words-in-use: Standard
case: Case file, illustrative. (a) A holding bought for Tk 100,000 on 1 July 2024 and sold for Tk 104,000 on 30 June 2025 after Tk 6,000 of income: return Tk 10,000, rate of return 10%. (b) The partners study two investments for surplus cash with three states of the economy: weak (probability 0.25), normal (0.50), strong (0.25). Investment X returns 6%, 8%, 10%; Investment Y returns 0%, 10%, 22%. Expected value: X 8.0%, Y 10.5%. Variance: X 2.0, Y 60.75. Standard deviation: X 1.41%, Y 7.79%. Coefficient of variation: X 0.18, Y 0.74. Investment Y offers more return and more risk, both in total and per unit of return.
history: Daniel Bernoulli, 1738 paper on measuring risk, which showed that people judge a gamble by its meaning to them as well as by its average. Search: Daniel Bernoulli 1738 Specimen theoriae novae risk.
refs: Chapter 5, 'Present Value and Discounting', section 5.2 'Mixed streams of cash flows' — averages of future sums; Chapter 10, 'Leverage', section 10.3 'Financial leverage' — how borrowing adds financial risk; Chapter 11, 'Required Return, CAPM and Market Efficiency', section 11.1 'Risk premium and required return' — pricing risk.
need: Chapter 4, 'Interest and Future Value': section 4.1 'Why time changes the value of money'; Chapter A1, 'Maths You Will Use': averages and percentages
ladder: 1 round numbers (two outcomes of equal chance); 2 three outcomes with unequal chances; 3 compare two investments with equal expected value but different spread, then with different expected values; 4 use the average, the spread and the risk-per-return ratio to rank three new assets
practice: review: define risk and say how business risk differs from financial risk, using a new firm; compute the expected value, then the variance, the standard deviation and the coefficient of variation, for a new two-asset table and state which is riskier per unit of return; explain standard deviation in plain words; think: an investor with Tk 200,000 must pick between the two assets in the Chapter 9 case and a third new asset; pause: after probability distribution, after standard deviation
sources: no

=== CH10 ===
title: Leverage
purpose: Teach break-even analysis and the three kinds of leverage, and show how borrowing and fixed costs magnify the effect of sales on earnings.
pace: slow — several moving parts (fixed costs, interest, preferred dividends, tax) in one chain
style: calculation
words: 4125
figures: 2
- fig01: a break-even chart of revenue, total cost and fixed cost against units sold
- fig02: the chain from a change in sales to a change in earnings for owners
plate: a long iron lever lifting a heavy stone block in a quarry, 1870s
sections:
10.1 | Costs and the break-even point | technique | 325
10.2 | Operating leverage | new idea | 550
10.3 | Financial leverage | new idea | 325
10.4 | Total leverage and risk | framework | 325
concepts:
- 10.1 | fixed and variable costs | minor | needs: business risk (Chapter 9)
- 10.1 | operating break-even point | standard | needs: fixed and variable costs
- 10.2 | degree of operating leverage | core | needs: operating break-even point
- 10.3 | degree of financial leverage | standard | needs: degree of operating leverage
- 10.3 | preferred stock | minor | needs: degree of financial leverage
- 10.4 | degree of total leverage | standard | needs: degree of financial leverage
- 10.4 | leverage and risk | minor | needs: degree of total leverage
defines:
- Leverage | The use of a fixed cost or fixed payment so that a small change in sales causes a larger change in earnings.
- Fixed cost | A cost that stays the same however many units are sold, such as shop rent.
- Variable cost | A cost that rises and falls with the number of units sold, such as the price paid for each book.
- Contribution margin | Selling price per unit minus variable cost per unit; it pays first for fixed costs, then gives profit.
- Break-even point | The sales volume at which total revenue equals total cost, so profit is zero.
- EBIT | Earnings before interest and tax: sales minus operating costs.
- Operating leverage | The effect of fixed operating costs on how EBIT responds to sales. Measured by the degree of operating leverage (DOL), the percentage change in EBIT divided by the percentage change in sales.
- Financial leverage | The effect of fixed financing payments on how owners' earnings respond to EBIT. Measured by the degree of financial leverage (DFL).
- Total leverage | The combined effect of operating and financial leverage on how owners' earnings respond to sales. Measured by the degree of total leverage (DTL), which equals DOL times DFL.
- Earnings per share | Earnings left for owners of common stock divided by the number of shares.
- Preferred stock | Shares that pay a fixed dividend, which must be paid before any dividend on common stock.
assumes: business risk; financial risk; profit; asset; liability; equity; dividend; risk; rate of return
words-in-use: Fixed; Variable
case: Case file, illustrative. The partners plan an own-label notebook line for 2026 and, from 1 July 2026, a conversion into a private company. Selling price Tk 90 a unit; variable cost Tk 55 a unit; fixed operating cost Tk 280,000 a year; interest Tk 60,000 a year (the Tk 600,000 bank loan at 10%); preferred dividends Tk 15,000 a year if the new company issues preferred stock; tax at an assumed 25% (rates differ by country and by kind of business). Sales 16,000 units. Contribution margin Tk 35. Break-even point 8,000 units. EBIT Tk 280,000. DOL 2.0. DFL 1.4 (280,000 / (280,000 - 60,000 - 15,000/0.75)). DTL 2.8. If sales rise 10% to 17,600 units, EBIT rises 20% to Tk 336,000 and earnings for owners of common stock rise 28%, from Tk 150,000 to Tk 192,000.
history: Long-Term Capital Management, whose heavy borrowing led to a rescue organised by the Federal Reserve Bank of New York on 23 September 1998. Search: Long-Term Capital Management 1998 leverage rescue.
refs: Chapter 9, 'Risk and Return', section 9.1 'Return and risk' — business risk and financial risk; Chapter 11, 'Required Return, CAPM and Market Efficiency', section 11.1 'Risk premium and required return' — what investors ask for when risk rises; Chapter 15, 'Long-Term Financing and the Capital Market', section 15.2 'Debt and equity as sources' — where fixed financing payments come from.
need: Chapter 9, 'Risk and Return': section 9.1 'Return and risk'; Chapter 2, 'The Financial Manager's Decisions': section 2.3 'Decisions on the balance sheet'
ladder: 1 round numbers (price Tk 10, variable cost Tk 6, fixed cost Tk 400); 2 realistic figures with interest and tax; 3 find break-even volume, EBIT at three volumes and the degree of operating leverage at each; 4 find all three degrees and trace a 10% sales change to owners' earnings
practice: review: say what leverage means and tell its three kinds apart with new data; find the break-even point and degrees of operating, financial and total leverage for a new firm; explain in plain words why high leverage raises risk; think: a firm has high fixed costs and heavy loans — what happens to owners' earnings if sales fall 10%; pause: after break-even point, after degree of operating leverage
sources: no

=== CH11 ===
title: Required Return, CAPM and Market Efficiency
purpose: Explain how risk is priced: risk premium, diversification, beta, the capital asset pricing model, and how well markets absorb information.
pace: standard — a connected set of ideas; the model itself is short
style: mixed
words: 4150
figures: 2
- fig01: the security market line with two investments plotted
- fig02: falling portfolio risk as the number of holdings grows, with a floor for market risk
plate: a cartographer's table with a coast chart, dividers and a brass compass, 1870s
sections:
11.1 | Risk premium and required return | new idea | 325
11.2 | Diversification and beta | new idea | 450
11.3 | The capital asset pricing model | defining theory | 550
11.4 | Efficient markets | framework | 225
concepts:
- 11.1 | risk premium | standard | needs: standard deviation (Chapter 9)
- 11.1 | risk-free rate | minor | needs: risk premium
- 11.2 | diversification and market risk | standard | needs: risk premium
- 11.2 | beta | standard | needs: diversification and market risk
- 11.3 | CAPM and the security market line | core | needs: beta
- 11.4 | market efficiency and its forms | standard | needs: CAPM and the security market line
defines:
- Required return | The least return an investor will accept for taking a given risk.
- Risk-free rate | The return on an investment with no risk of loss, such as a short-term government security.
- Risk premium | The extra return demanded for taking risk instead of a risk-free investment.
- Portfolio | A collection of investments held together by one investor.
- Diversification | Spreading money across many investments so that one failure does less damage.
- Systematic risk | Risk that affects all investments, such as a recession; it cannot be diversified away.
- Unsystematic risk | Risk that affects one firm or industry only; diversification can remove it.
- Beta | A number showing how strongly an investment's return moves with the market; 1.0 means it moves with the market.
- Market return | The average return of all investments in a market during a period.
- Capital asset pricing model | A formula for required return: risk-free rate plus beta times the market risk premium.
- Security market line | The graph of the capital asset pricing model, with beta on one axis and required return on the other.
- Efficient market | A market in which prices already reflect the available information.
assumes: risk; return; rate of return; expected value; standard deviation; coefficient of variation; business risk; financial risk; time value of money
words-in-use: Market
case: Case file, illustrative. Assumed market data for October 2025: risk-free rate 6%; market return 12%; market risk premium 6%. Investments from Chapter 9 with assumed betas: X beta 0.3, required return 6 + 0.3 x 6 = 7.8%, expected return 8.0%, so acceptable; Y beta 1.2, required return 6 + 1.2 x 6 = 13.2%, expected return 10.5%, so rejected. A listed paper-and-printing company, beta 1.25: required return 6 + 1.25 x 6 = 13.5%.
history: William Sharpe's 1964 paper on capital asset prices, and the 1990 Nobel Prize in economics shared by Markowitz, Miller and Sharpe. Search: Sharpe 1964 Capital asset prices theory market equilibrium.
refs: Chapter 9, 'Risk and Return', section 9.3 'Measuring risk' — standard deviation as the risk measure; Chapter 13, 'Valuation of Shares', section 13.3 'Valuing common stock' — required return used as the discount rate; Chapter 15, 'Long-Term Financing and the Capital Market', section 15.4 'The cost of capital' — equity cost.
need: Chapter 9, 'Risk and Return': sections 9.1 'Return and risk', 9.2 'Describing uncertainty' and 9.3 'Measuring risk'
ladder: 1 round numbers (risk-free 5%, market 10%, beta 1); 2 realistic figures with beta above and below 1; 3 compare expected and required return to accept or reject; 4 combine with Chapter 9 expected value and with a shift in market return
practice: review: explain risk premium and why investors demand it, with new figures; separate systematic from unsystematic risk using a new list of risks; compute required return for three new betas; describe the three forms of market efficiency and what each implies; think: a fund holds 40 shares yet is still exposed to the market — explain; pause: after risk premium, after beta
sources: yes

=== CH12 ===
title: Valuation of Bonds
purpose: Teach valuation as the present value of future cash and apply it to bonds, including semiannual interest, yield to maturity and the premium, discount and par forms.
pace: standard — builds directly on annuities and discounting
style: calculation
words: 4150
figures: 2
- fig01: a bond's cash flows on a timeline: interest each year and face value at the end
- fig02: bond price falling as the required return rises
plate: a bundle of bonds tied with ribbon and a wax seal on a lawyer's desk, 1880s
sections:
12.1 | The idea of valuation | new idea | 550
12.2 | What a bond is | framework | 225
12.3 | Pricing a bond | technique | 325
12.4 | Yield and price | framework | 450
concepts:
- 12.1 | value as present value of future cash | core | needs: present value of an ordinary annuity (Chapter 6)
- 12.2 | bond and its features | standard | needs: value as present value of future cash
- 12.3 | value of an annual-interest bond | standard | needs: bond and its features
- 12.3 | semiannual interest | minor | needs: value of an annual-interest bond
- 12.4 | yield to maturity | standard | needs: value of an annual-interest bond
- 12.4 | premium, discount and par | standard | needs: yield to maturity
defines:
- Valuation | Finding what an asset is worth today by adding the present values of the cash it will bring.
- Bond | A loan made to a company or government, repaid on a set date, with interest paid on the way.
- Face value | The amount a bond repays at its end, for example Tk 1,000.
- Coupon rate | The yearly interest of a bond, as a percentage of its face value.
- Maturity | The date on which a bond or loan must be repaid.
- Yield to maturity | The yearly return an investor earns by buying a bond at today's price and holding it to maturity.
- Premium bond | A bond that sells for more than its face value.
- Discount bond | A bond that sells for less than its face value.
- Semiannual interest | Interest paid twice a year, each payment being half the yearly amount.
assumes: present value; discounting; discount rate; annuity; ordinary annuity; required return; interest; interest rate; risk-free rate; cash inflow; factor table
words-in-use: Par; Coupon; Premium
case: Case file, illustrative. The partners study an illustrative five-year bond, face value Tk 1,000, coupon rate 9% paid once a year (Tk 90). Required return 12%: value Tk 891.86 (a discount bond). Required return 8%: value Tk 1,039.93 (a premium bond). Required return 9%: value Tk 1,000.00 (selling at face value). If interest is paid every six months at 12% a year (ten periods of 6%, Tk 45 each): value Tk 889.60.
history: British consols, perpetual bonds first issued in the 1750s, and the UK government's redemption of its 3.5% War Loan in 2015. Search: British consols history redemption War Loan 2015.
refs: Chapter 6, 'Annuities', section 6.3 'Present value of an annuity' — the interest stream; Chapter 11, 'Required Return, CAPM and Market Efficiency', section 11.1 'Risk premium and required return' — the required return used to discount; Chapter 15, 'Long-Term Financing and the Capital Market', section 15.2 'Debt and equity as sources' — bonds as a source of funds.
need: Chapter 5, 'Present Value and Discounting': section 5.1 'Discounting a single sum'; Chapter 6, 'Annuities': section 6.3 'Present value of an annuity'; Chapter 11, 'Required Return, CAPM and Market Efficiency': section 11.1 'Risk premium and required return'
ladder: 1 round numbers (face value Tk 100, coupon 10%, required return 10%); 2 realistic five- and ten-year bonds at different required returns; 3 semiannual interest and a find-the-yield question; 4 compare several bonds in one table and say which sell at a premium, discount or par
practice: review: explain what a bond is and name its main features with a new issue; compute the value of three new bonds paying interest yearly and say whether each is at a premium, discount or par; explain the link between coupon rate, required return and price; define yield to maturity in plain words; think: a bond's price falls after the market lifts required returns — explain what the holder has lost; pause: after bond features, after pricing
sources: no

=== CH13 ===
title: Valuation of Shares
purpose: Describe common stock and value preferred and common stock from the dividends they are expected to pay.
pace: standard — applies Chapter 12 valuation to a different cash stream
style: mixed
words: 4025
figures: 1
- fig01: a stream of dividends growing at a steady rate from year to year
plate: a stock exchange floor with brokers and a chalk board of prices, 1890s
sections:
13.1 | Common stock | framework | 325
13.2 | Valuing preferred stock | technique | 325
13.3 | Valuing common stock | technique | 775
concepts:
- 13.1 | common stock | standard | needs: preferred stock (Chapter 10)
- 13.1 | stock compared with bond | minor | needs: common stock
- 13.2 | perpetuity | minor | needs: present value of an ordinary annuity (Chapter 6)
- 13.2 | value of preferred stock | standard | needs: perpetuity
- 13.3 | dividend valuation | core | needs: value as present value of future cash (Chapter 12)
- 13.3 | constant dividend growth | standard | needs: dividend valuation
defines:
- Common stock | Shares that give owners a vote and a claim on profit after all other claims are met.
- Residual claim | The right to whatever is left after lenders and preferred owners have been paid.
- Capital gain | The profit from selling an asset for more than its purchase price.
- Perpetuity | A series of equal payments that continues for ever.
- Dividend valuation model | A way of valuing a share as the present value of the dividends it is expected to pay.
- Constant growth model | The dividend valuation model for dividends that grow at the same rate every year.
assumes: valuation; bond; face value; coupon rate; required return; present value; discounting; annuity; preferred stock; dividend; shareholder; share price; company; risk premium
words-in-use: Share; Growth
case: Case file, illustrative. Assumed figures for the listed paper-and-printing company of Chapter 11: last yearly dividend Tk 5.00 a share; expected growth 6% a year; required return 13.5% (from Chapter 11). Next dividend Tk 5.30 (5.00 x 1.06). Constant growth value Tk 70.67 (5.30 / (0.135 - 0.06)). If dividends did not grow, value Tk 37.04 (5.00 / 0.135). A preferred stock paying Tk 8 a year for ever with a required return of 10% is worth Tk 80.00.
history: The South Sea Company of 1720: its share price rose and collapsed in one year while its earnings stayed small. Valuation theory: John Burr Williams, The Theory of Investment Value (1938) and Myron Gordon (1959). Search: South Sea Bubble 1720 share price; Williams 1938 investment value.
refs: Chapter 12, 'Valuation of Bonds', section 12.1 'The idea of valuation' — the principle used; Chapter 11, 'Required Return, CAPM and Market Efficiency', section 11.3 'The capital asset pricing model' — the required return; Chapter 15, 'Long-Term Financing and the Capital Market', section 15.2 'Debt and equity as sources' — stock as a source of money.
need: Chapter 12, 'Valuation of Bonds': sections 12.1 'The idea of valuation' and 12.2 'What a bond is'; Chapter 11, 'Required Return, CAPM and Market Efficiency': section 11.3 'The capital asset pricing model'
ladder: 1 round numbers (dividend Tk 10 for ever at 10%); 2 constant growth with realistic figures; 3 compare value with market price and decide; 4 value preferred and common stock of one firm and compare their risk and required returns
practice: review: say how common stock differs from a bond using a new firm; value a preferred stock and a growing common stock from new data; explain why growth raises value but also needs a required return above growth; think: price is above your computed value — list reasons and decide; pause: after common stock, after perpetuity
sources: yes

=== CH14 ===
title: Working Capital and Short-Term Financing
purpose: Explain working capital, how to finance it with short-term sources, how to price trade credit, and how to estimate what a business needs.
pace: standard — many terms, each simple; the cash conversion cycle needs care
style: mixed
words: 4475
figures: 2
- fig01: a timeline of the operating cycle and cash conversion cycle
- fig02: permanent and temporary financing needs matched to long-term and short-term sources
plate: a warehouse with sacks, crates and a weighing machine watched by a clerk, 1880s
sections:
14.1 | Working capital and how to finance it | framework | 550
14.2 | Sources of short-term finance | framework | 775
14.3 | Cycles, float and estimating needs | technique | 550
concepts:
- 14.1 | working capital | standard | needs: balance-sheet view of the firm (Chapter 2)
- 14.1 | matching principle | standard | needs: working capital
- 14.1 | short, intermediate and long maturities | minor | needs: working capital
- 14.2 | trade credit and its cost | core | needs: matching principle
- 14.2 | bank loans and other short-term sources | standard | needs: trade credit and its cost
- 14.3 | operating cycle and cash conversion cycle | standard | needs: working capital
- 14.3 | float | minor | needs: operating cycle and cash conversion cycle
- 14.3 | estimating working capital need | standard | needs: operating cycle and cash conversion cycle
defines:
- Working capital | The money a business has tied up in everyday trading: cash, stock and money owed to it.
- Net working capital | Current assets minus current liabilities; what remains for trading after short debts are paid.
- Matching principle | Pay for short-lived needs with short-term money and for lasting needs with long-term money.
- Short-term financing | Money borrowed to be repaid within one year.
- Intermediate-term financing | Money borrowed to be repaid in more than one year but not more than about five.
- Long-term financing | Money raised for more than about five years, or with no fixed repayment date.
- Trade credit | Credit from a supplier who lets a buyer pay some days after delivery.
- Cash discount | A price cut a supplier gives for paying early, such as 2% off if paid within 10 days.
- Inventory | The goods a business holds for sale, such as the books on a shop's shelves.
- Accounts receivable | Money that customers owe a business for goods already delivered.
- Accounts payable | Money a business owes its suppliers for goods already received.
- Operating cycle | The days from buying stock to collecting cash from its sale.
- Cash conversion cycle | The operating cycle minus the days a business takes to pay its suppliers.
- Float | Money tied up in payments that are sent but not yet usable, such as a cheque in the post.
assumes: cash flow; asset; liability; balance sheet; interest rate; maturity; financing decision; profit; time value of money
words-in-use: Current; Cycle
case: Case file, illustrative. Balance sheet of 30 June 2025 (Chapter 2): cash Tk 180,000; school invoices Tk 250,000; stock Tk 1,350,000; supplier bills Tk 430,000; the Tk 600,000 bank loan is long-term. Current assets Tk 1,780,000; net working capital Tk 1,350,000 (1,780,000 - 430,000). A supplier offers terms 2/10, net 40 on a Tk 100,000 invoice (2% off if paid in 10 days, otherwise due in 40). Cost of giving up the discount: 24.83% a year (2/98 x 365/30). A bank overdraft costs 14% a year, so the shop should take the discount and borrow. Days, rounded: stock 180 days, school invoices 22 days, supplier bills 58 days; operating cycle 202 days; cash conversion cycle 144 days. Yearly cash operating costs Tk 3,880,000 (2,730,000 + 1,150,000). Working capital to be financed = 3,880,000 x 144 / 365 = Tk 1,530,739.73.
history: Toyota's just-in-time system, developed from the late 1940s by Taiichi Ohno and others to cut stock held. Search: Toyota just-in-time Taiichi Ohno inventory history.
refs: Chapter 2, 'The Financial Manager's Decisions', section 2.3 'Decisions on the balance sheet' — the items that make up working capital; Chapter 4, 'Interest and Future Value', section 4.2 'Simple and compound interest' — turning a discount into a yearly rate; Chapter 15, 'Long-Term Financing and the Capital Market', section 15.1 'Term loans and the features of financing' — the long-term end of the matching principle.
need: Chapter 2, 'The Financial Manager's Decisions': section 2.3 'Decisions on the balance sheet'; Chapter 4, 'Interest and Future Value': section 4.2 'Simple and compound interest'
ladder: 1 round numbers (stock 30 days, receivables 20 days, payables 10 days); 2 realistic days from yearly figures; 3 compare giving up and taking a cash discount against a bank rate; 4 estimate the money needed for a growing firm and choose short or long-term sources by the matching principle
practice: review: say what working capital is and why a profitable firm can still run short; compute the cost of giving up a cash discount for new terms and recommend the cheaper source; find the cash conversion cycle and the financing need for new data; define float and its parts in plain words; think: a seasonal toy seller needs extra stock for three months — choose the sources; pause: after matching principle, after cash conversion cycle
sources: no

=== CH15 ===
title: Long-Term Financing and the Capital Market
purpose: Describe the sources of long-term money for a business, how a company raises money in the capital market, the institutions that supply it in Bangladesh, and the cost of that money.
pace: standard — descriptive and wide; each source is one idea
style: descriptive
words: 4275
figures: 1
- fig01: a map of the sources of long-term finance: borrowing, outside owners and retained earnings
plate: an iron foundry with a glowing furnace and men pouring molten metal, 1870s
sections:
15.1 | Term loans and the features of financing | framework | 450
15.2 | Debt and equity as sources | framework | 550
15.3 | Raising funds in the capital market | framework | 450
15.4 | The cost of capital | technique | 225
concepts:
- 15.1 | term loans | standard | needs: long-term financing (Chapter 14)
- 15.1 | general characteristics of financing | standard | needs: term loans
- 15.2 | methods of long-term debt | standard | needs: general characteristics of financing
- 15.2 | preferred stock, common stock and retained earnings as sources | standard | needs: methods of long-term debt
- 15.2 | retained earnings | minor | needs: preferred stock, common stock and retained earnings as sources
- 15.3 | raising funds from the capital market | standard | needs: preferred stock, common stock and retained earnings as sources
- 15.3 | institutions supplying long-term finance in Bangladesh | standard | needs: raising funds from the capital market
- 15.4 | cost of capital | standard | needs: general characteristics of financing
defines:
- Term loan | A loan repaid in regular instalments over a fixed number of years, usually from a bank.
- Collateral | An asset a lender may take if the borrower fails to repay.
- Covenant | A condition in a loan agreement that the borrower promises to keep.
- Debenture | A bond backed only by the issuer's general promise to pay, not by a particular asset.
- Retained earnings | Profit kept in the business instead of being paid out as dividends.
- Capital market | The market in which long-term money is raised by selling bonds and shares.
- Initial public offering | A company's first sale of shares to the public.
- Rights issue | An offer of new shares to existing shareholders, in proportion to their holdings.
- Underwriter | An institution that promises to buy any shares of a new issue that the public does not.
- Cost of capital | The return a firm must earn on its investments to satisfy those who supply its money.
- Weighted average cost of capital | The average cost of a firm's different sources of money, each weighted by its share of the total.
assumes: long-term financing; intermediate-term financing; maturity; bond; common stock; preferred stock; dividend; required return; interest rate; discount rate; financing decision; leverage; financial risk
words-in-use: Term; Security
case: Case file, illustrative. Decision of 5 January 2026: a second branch costing Tk 2,000,000. Proposed financing: term loan Tk 800,000 (40%), repaid over five years at 10% a year, secured on fittings and stock; owners' funds Tk 1,200,000 (60%), made up of retained earnings of Tk 200,000 (from Chapter 2) and Tk 1,000,000 new money from the partners. Assumed tax rate 25%. After-tax cost of the loan 7.5% (10% x (1 - 0.25)). Cost of owners' funds 13.5% (Chapter 11, taken as given). Weighted average cost of capital 11.1% (0.4 x 7.5 + 0.6 x 13.5). Institutions: state and private banks, development finance institutions, the stock exchanges and the securities regulator; the chapter writer confirms current names and roles.
history: Dhaka Stock Exchange: its share-price boom of 2010 and the sharp fall of early 2011. Search: Dhaka Stock Exchange 2010 boom 2011 crash index.
refs: Chapter 10, 'Leverage', section 10.3 'Financial leverage' — fixed financing payments; Chapter 12, 'Valuation of Bonds', section 12.2 'What a bond is' — bonds as debt; Chapter 11, 'Required Return, CAPM and Market Efficiency', section 11.3 'The capital asset pricing model' — cost of owners' funds.
need: Chapter 14, 'Working Capital and Short-Term Financing': section 14.1 'Working capital and how to finance it'; Chapter 12, 'Valuation of Bonds': section 12.2 'What a bond is'; Chapter 13, 'Valuation of Shares': section 13.1 'Common stock'
ladder: 1 a family borrowing to buy a house, then asking relatives for money (familiar case); 2 a bakery choosing between a bank term loan and retained profit (reshaped case); 3 a growing Bangladeshi company choosing between a rights issue and an initial public offering (new setting); 4 a bookshop financing a branch from three sources, combining Chapters 10, 11 and 14
practice: review: sort given facts into short, intermediate and long-term financing; describe the main sources of long-term money for a new company with their strengths and limits; explain what retained earnings cost the firm; compute the weighted average cost of capital for new figures; think: a start-up has no profit history — rank its realistic sources of long-term money; pause: after the features of financing, after capital-market issues
sources: no

=== CH16 ===
title: Leasing
purpose: Explain what a lease is, the kinds of lease, and how to compare leasing with buying using after-tax cash flows.
pace: standard — the comparison reuses discounting and tax from earlier chapters
style: mixed
words: 3800
figures: 1
- fig01: after-tax cash outflows of leasing and of buying a van, year by year
plate: a carriage-hire yard with several carriages and a stable hand at work, 1880s
sections:
16.1 | What leasing is | framework | 225
16.2 | Kinds of lease | framework | 325
16.3 | The lease-or-buy decision | technique | 650
concepts:
- 16.1 | lease | standard | needs: financing decision (Chapter 2)
- 16.2 | operating and financial leases | standard | needs: lease
- 16.2 | other lease forms | minor | needs: operating and financial leases
- 16.3 | lease-versus-purchase steps and after-tax cash outflows | core | needs: present value of an ordinary annuity (Chapter 6)
- 16.3 | tax effects | minor | needs: lease-versus-purchase steps and after-tax cash outflows
defines:
- Lease | A contract in which the owner of an asset lets another party use it for regular payments.
- Lessor | The owner who lets the asset out under a lease.
- Lessee | The user who pays to use the asset under a lease.
- Operating lease | A short lease, cancellable, where the lessor keeps most of the risks of owning the asset.
- Financial lease | A long lease, not cancellable, that covers most of the asset's life and works like a loan.
- Sale-and-leaseback | A deal in which a firm sells an asset it owns and leases it back from the buyer.
- Tax shield | The tax saved because a cost, such as interest or depreciation, reduces taxable income.
- After-tax cash outflow | A payment's cost after subtracting the tax it saves.
assumes: present value; discounting; annuity; ordinary annuity; instalment; depreciation; interest rate; financing decision; cost of capital; term loan
words-in-use: Rental
case: Case file, illustrative. Decision of 1 March 2026: a delivery van with a price of Tk 800,000. Lease: Tk 190,000 at the end of each year for five years, maintenance paid by the lessor. Purchase: a loan of Tk 800,000 at 10% repaid in five equal year-end instalments of Tk 211,037.98; depreciation Tk 160,000 a year (no scrap value); maintenance Tk 20,000 a year paid by the owner. Assumed tax rate 25%. Discount rate 7.5%, the after-tax cost of the loan (Chapter 15). Present value of after-tax outflows: lease Tk 576,538.60; purchase Tk 698,852.88. On these figures leasing costs less by Tk 122,314.28.
history: United States Leasing Corporation, founded in San Francisco in 1952, an early firm of the modern equipment-leasing industry. Search: United States Leasing Corporation 1952 Boothe San Francisco.
refs: Chapter 15, 'Long-Term Financing and the Capital Market', section 15.4 'The cost of capital' — the discount rate; Chapter 6, 'Annuities', section 6.3 'Present value of an annuity' — valuing the lease payments; Chapter 7, 'Capital Budgeting: Process and Cash Flows', section 7.3 'Cash flows from an investment' — depreciation and tax.
need: Chapter 6, 'Annuities': section 6.3 'Present value of an annuity'; Chapter 7, 'Capital Budgeting: Process and Cash Flows': section 7.3 'Cash flows from an investment'; Chapter 15, 'Long-Term Financing and the Capital Market': section 15.4 'The cost of capital'
ladder: 1 round numbers (lease Tk 100 a year for three years at 10%, no tax); 2 realistic five-year lease with tax; 3 add a loan schedule and depreciation for the purchase option; 4 compare two lease offers against purchase and decide
practice: review: say what a lease is and compare operating and financial leases with a new asset; list the steps of the lease-or-buy comparison; compute the after-tax present value of a new lease and purchase; explain the tax shield of interest and depreciation; think: a lease is cheaper on cost but cancellable only with a penalty — weigh it; pause: after kinds of lease, after after-tax outflows
sources: no

=== A1 ===
title: Maths You Will Use
purpose: Give a short reference for the arithmetic used in the book, with one tiny example each.
pace: standard — reference, not a lesson
style: calculation
words: 1000
figures: 0
sections:
A1.1 | Percentages and percentage change | reference | 200
A1.2 | Ratios and averages | reference | 200
A1.3 | Rearranging an equation and rounding | reference | 300
A1.4 | Reading a graph | reference | 300
concepts:
- A1.1 | percentage and percentage change | minor | needs: none
- A1.2 | ratio and average | minor | needs: none
- A1.3 | rearranging and rounding | minor | needs: none
- A1.4 | reading a graph | minor | needs: none
defines: none
assumes: none
words-in-use: none
case: none
history: none
refs: Chapter 4, 'Interest and Future Value', section 4.2 'Simple and compound interest' — percentages in use; Chapter 9, 'Risk and Return', section 9.2 'Describing uncertainty' — averages in use
need: nothing
ladder: 1 one-step example; 2 two-step example
practice: none
sources: no
