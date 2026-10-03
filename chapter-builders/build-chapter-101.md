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
course: MGT 101
book: MGT 101
spelling: British · dates: day, month, year (12 March 2026) · country: mixed, no single country; the running case's home is Bangladesh; name the place whenever law or standards differ · currency and numbers: taka for the running case, written Tk 158,000 (international digit grouping); a historical case keeps its own currency
running case: Meghna and Sons, a family-run bookshop in Dhaka — illustrative documented case file. Base facts (FIXED): Rafiq Uddin Mia opened the bookshop on 4 January 2015 as sole proprietor, with Tk 158,000 of his own savings. The name comes from the river near his home village. Later steps in the case are given in each chapter's entry.
chosen words (one term, one word):
- use business — also called enterprise, firm, concern
- use company — also called joint stock company, corporation (the words public corporation and multinational corporation keep their own meaning)
- use owner — also called proprietor (except in the term sole proprietorship)
- use customer — also called buyer, client
- use supplier — also called vendor, seller of inputs
- use profit — also called gain, net earnings (a cooperative society uses surplus)
- use shareholder — also called stockholder
- use board of directors — also called board
- use state enterprise — also called public enterprise, state-owned enterprise
- use foreign trade — also called international trade
- use stock exchange — also called share bourse
- use sleeping partner — also called dormant partner
- use export processing zone — no short form until it is defined in full
- use parent-country national, host-country national, third-country national — also written PCN, HCN, TCN after the full terms are defined
size plan: 12 chapters plus appendix A1, ~57,225 words, ~242 pages
chapters:
1. What Business Is, Does and Aims For
2. Resources, Location and Environment
3. Social Responsibility of Business
4. Ways to Own a Business, and the Sole Proprietor
5. Partnership
6. Joint Stock Company
7. Cooperative Societies
8. State Enterprise
9. The Share Market
10. Foreign Trade: Measuring It and Doing It
11. Multinational Corporations
12. Institutions and Business Combination
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
title: What Business Is, Does and Aims For
purpose: Show a reader with no background what a business is, how trade, commerce and industry fit together, and why businesses exist; this is a foundation chapter that also teaches how to read the book.
pace: slow — every term is new, and the chapter teaches the reader how to use side notes, recaps and pause questions
style: descriptive
words: 5475
figures: 1
- fig01: the chain from maker to trader to customer, with the helping services (transport, storage, banking, insurance, advertising) drawn beside it
plate: a village market square with a stallholder weighing grain for a customer, 1860s
sections:
1.1 | Needs, Wants and Exchange | new idea | 775
1.2 | What a Business Is | new idea | 775
1.3 | Trade, Commerce and Industry | framework | 775
1.4 | Features, Functions and Aims of Business | framework | 550
concepts:
- 1.1 | Needs and wants, and why people must choose | core | needs: none
- 1.1 | Exchange, and why people let others make things for them | standard | needs: needs and wants
- 1.2 | Business as the supply of goods and services for profit | core | needs: exchange
- 1.2 | Profit and risk | standard | needs: business
- 1.3 | Trade, commerce and industry, and how they fit together | core | needs: business
- 1.3 | Branches of business and the helping services, including selling online | standard | needs: trade, commerce, industry
- 1.4 | Scope, features, functions and aims of business, and the conditions that help it succeed | core | needs: profit and risk
defines:
- Need | something a person must have to live safely and in health, such as food, water, shelter and basic care
- Want | something a person would like to have but could live without, such as a new phone or a holiday
- Exchange | giving one thing and receiving another in return, whether goods, services or money
- Good | a physical item that can be touched and owned, such as a book, a chair or a bag of rice
- Service | useful work done for another person that leaves nothing physical behind, such as teaching, carrying or repairing
- Business | an activity that supplies goods or services to customers in the hope of earning a profit
- Profit | the money left over when the costs of running a business are taken away from what it earns
- Risk | the chance that a business will earn less than it hoped, or lose money, because the future is uncertain
- Trade | the buying and selling of goods, either to make a profit or to supply what others want
- Commerce | all the activities that help goods move from maker to user, including trade and the services that support it
- Industry | the making or growing of goods, or the extraction of materials, by people who use skill, tools and effort
assumes: none
words-in-use: industry, profit, trade
case: Base facts. Rafiq Uddin Mia opened Meghna and Sons, a bookshop in Dhaka, on 4 January 2015. Start-up money was Tk 158,000 of his own savings, used as follows: books for sale Tk 110,000 (500 textbooks bought at an average Tk 220 each); advance paid to the landlord Tk 30,000; shelves and counter Tk 12,000; cash in hand Tk 6,000 (110,000 + 30,000 + 12,000 + 6,000 = 158,000). Average selling price Tk 280 per book, so each book sold earns Tk 60 above its cost. Monthly shop rent Tk 9,000. In January 2015 the shop sold 180 books: sales Tk 50,400 (180 x 280); cost of the books sold Tk 39,600 (180 x 220); amount left above book cost Tk 10,800. After rent of Tk 9,000 the profit for the month was Tk 1,800. Unsold at 31 January 2015: 320 books with a cost of Tk 70,400 (320 x 220). Rafiq took no wage for himself that month.
history: Adam Smith, An Inquiry into the Nature and Causes of the Wealth of Nations, 1776: the pin-making example of workers who specialise and exchange. Search hint: Adam Smith pin factory 1776 division of labour.
refs: Chapter 2, 'Resources, Location and Environment', section 2.1 'The Factors of Production' — the resources that every business uses to make or sell; Chapter 12, 'Institutions and Business Combination', section 12.1 'Institutions That Promote Business' — bodies that support trade and industry
need: nothing
ladder: a household choosing what to buy this week; the same choices made by a market stall; a village weaver selling cloth across a river (new setting); a business weighing its own profit against what its town needs (combined case)
practice: review: sort a student's week of spending into needs and wants and say why the sorting is hard; explain exchange using two villagers who each make one thing; name the branch of business for a printing press, a wholesaler and an insurer; explain why money received and profit are different amounts; think: a tea stall owner could earn more by selling only cold drinks, yet her neighbours rely on hot tea, so weigh profit against service and decide; pause: after the passage on needs and wants, and after the passage separating trade, commerce and industry
sources: no

=== CH02 ===
title: Resources, Location and Environment
purpose: Teach the resources every business draws on, how a business chooses where to operate, and how the world around it shapes what it can do.
pace: slow — three new abstract ideas (factors, location, environment) arrive in a short chapter
style: descriptive
words: 4475
figures: 1
- fig01: a business at the centre with the internal group (owner, helper, resources) close in and the outside forces (customers, rivals, government, technology, economy, society) in a ring around it
plate: a surveyor with a theodolite at a river bend beside a mill and a railway line, 1870s
sections:
2.1 | The Factors of Production | new idea | 775
2.2 | Choosing a Location | framework | 550
2.3 | The Business Environment | framework | 550
concepts:
- 2.1 | The four factors of production and the reward each earns | core | needs: business
- 2.1 | How the factors are combined by the entrepreneur | standard | needs: factors of production
- 2.2 | The forces that shape where a business sets up, and how to weigh them | core | needs: factors of production
- 2.3 | Internal and external environment, and how a business and its surroundings affect each other | core | needs: business, risk
defines:
- Factors of production | the resources a business must combine to make or sell anything: land, labour, capital and the entrepreneur
- Land | all natural resources and the ground itself, including soil, water, minerals and the site of a shop
- Labour | the physical and mental effort that people give to producing goods or services
- Capital | the money and the man-made means of production, such as tools, stock and buildings, used to earn more
- Entrepreneur | the person who combines the other resources, takes the risk and organises a business to meet a need
- Location | the place where a business carries out its work, chosen from the available sites
- Plant | the factory, machinery and equipment that a business uses to make its goods
- Environment | everything outside and around a business that can affect it, and everything inside that it controls
- Internal environment | the parts of the environment that the business controls: owners, managers, employees, methods and resources
- External environment | the forces outside the business that it cannot control but must respond to
assumes: business, profit, risk, trade, industry
words-in-use: capital, land, plant
case: Carried forward. Meghna and Sons opened on 4 January 2015 with start-up money of Tk 158,000 and monthly shop rent of Tk 9,000. Factors in the shop: land is the rented room (rent Tk 9,000 a month, advance paid to the landlord Tk 30,000); labour is Rafiq Uddin Mia and one helper, Mahbub, employed from 1 February 2015 at Tk 6,000 a month; capital is the Tk 158,000; Rafiq acts as entrepreneur. Location choice made in December 2014, three sites compared: Site A near a college: rent Tk 9,000, advance Tk 30,000, about 1,200 passers-by a day; Site B in a wholesale lane: rent Tk 14,000, advance Tk 56,000, about 2,000 passers-by a day; Site C in a residential lane: rent Tk 5,000, advance Tk 15,000, about 300 passers-by a day. Rent per 100 daily passers-by: Site A Tk 750, Site B Tk 700, Site C Tk 1,667 (to the nearest taka). Rafiq chose Site A because Site B's advance of Tk 56,000 was more than a third of his Tk 158,000 and its rent was Tk 5,000 higher. Environment events: on 2 January 2017 the education board changed the prescribed textbooks for three school classes, leaving 60 titles unsellable; average monthly sales were Tk 200,000 in 2017 and Tk 170,000 in 2018, a fall of 15% after an online bookstore began delivering in Dhaka; from March 2019 the helper delivered orders by bicycle for Tk 30 an order.
history: Tata Iron and Steel Company, 1907: the search for a site with ore, coal and water that ended at Sakchi, later Jamshedpur, India. Search hint: Tata Steel Sakchi site selection 1907 Jamshedpur.
refs: Chapter 1, 'What Business Is, Does and Aims For', section 1.2 'What a Business Is' — the idea of business that these resources serve; Chapter 3, 'Social Responsibility of Business', section 3.1 'Meaning and Importance of Responsibility' — the society that is part of the external environment
need: Chapter 1, 'What Business Is, Does and Aims For', section 1.2 'What a Business Is' and section 1.3 'Trade, Commerce and Industry'
ladder: a family kitchen as a small producer of meals (familiar); the bookshop's four factors (reshaped); a fish farm choosing a pond site near a river (new setting); a business choosing a site while a new rival and a change in rules arrive (combined case)
practice: review: name the four factors and the reward each one earns; list the forces that shape a location and say which matter most for a shop and which for a factory; separate a business's internal from its external environment, with an example of each; explain how a business can respond to a change it cannot control; think: a bakery can rent a roadside plot at Tk 18,000 a month with 2,400 daily passers-by, or an inner lane plot at Tk 7,000 with 500, and has Tk 120,000 to start, so compare rent per 100 passers-by and decide; pause: after the four factors, and after the split between internal and external environment
sources: no

=== CH03 ===
title: Social Responsibility of Business
purpose: Explain why a business owes duties beyond profit, to whom it owes them, and how a reader can recognise a responsible business.
pace: slow — the third chapter of the book; the ideas are familiar, but the reader is still learning to use the side notes and pause questions
style: descriptive
words: 4375
figures: 1
- fig01: a business in the middle with arrows to customers, employees, suppliers, lenders, owners and the community, each arrow labelled with the duty owed
plate: a mill-owner's committee inspecting a workers' school and reading room, 1880s
sections:
3.1 | Meaning and Importance of Responsibility | new idea | 775
3.2 | Responsibility to Society, Suppliers and Investors | framework | 775
3.3 | Recognising a Responsible Organisation | framework | 225
concepts:
- 3.1 | Social responsibility and the reasons it matters, including how it fits with the aim of profit | core | needs: profit, business
- 3.1 | Stakeholders and the idea of duties to each | standard | needs: social responsibility
- 3.2 | Duties to society, suppliers and investors | core | needs: stakeholders
- 3.2 | Business ethics in everyday decisions | standard | needs: social responsibility
- 3.3 | Signs that a business is acting responsibly | standard | needs: duties to stakeholders
defines:
- Social responsibility | the duty of a business to act in ways that benefit society as well as itself
- Stakeholder | any person or group affected by a business or able to affect it, such as customers or neighbours
- Supplier | a person or business that sells the goods, materials or services that another business needs
- Investor | a person or organisation that puts money into a business in the hope of getting more money back
- Business ethics | the standards of right and wrong that guide how a business treats people and makes decisions
assumes: business, profit, environment, external environment, capital
words-in-use: none
case: Carried forward. In 2019 Meghna and Sons had average monthly sales of Tk 190,000, so annual sales were Tk 2,280,000 (190,000 x 12). The helper, Mahbub, earned Tk 8,000 a month and received a festival bonus of one month's wage at each of two festivals, Tk 16,000 in the year (8,000 x 2). The shop paid its main supplier, a publisher called Alo Prokashoni (illustrative), within the agreed 45 days; the invoice of Tk 84,000 dated 1 June 2019 was paid on 15 July 2019, on day 44. On 1 March 2019 Rafiq Uddin Mia borrowed Tk 60,000 from a bank at 10% a year, so yearly interest was Tk 6,000. On 10 December 2019 the shop gave 1% of the year's sales, Tk 22,800 (2,280,000 x 1/100), to the library of a primary school. The shop has no outside investor; the bank is its only lender.
history: The collapse of the Rana Plaza building at Savar, Bangladesh, on 24 April 2013, and the building and fire safety agreement signed by buyers and unions in May 2013. Search hint: Rana Plaza collapse 2013 Accord on Fire and Building Safety.
refs: Chapter 2, 'Resources, Location and Environment', section 2.3 'The Business Environment' — the society and the economy as outside forces; Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', section 4.1 'Why the Form of Ownership Matters' — who answers for the business
need: Chapter 1, 'What Business Is, Does and Aims For', section 1.4 'Features, Functions and Aims of Business'; Chapter 2, 'Resources, Location and Environment', section 2.3 'The Business Environment'
ladder: a neighbour who borrows and returns tools fairly (familiar); the bookshop's duties to its helper, supplier and bank (reshaped); a garment factory and its buyers across borders (new setting); a business facing a conflict between a cheaper supplier and a safer one (combined case)
practice: review: say in your own words what social responsibility means and give two reasons it matters; name five stakeholders of a restaurant and the duty owed to each; explain what a business owes a supplier and what it owes an investor; list three signs of a responsible business; think: a printer offers books at 12% less, but its workers have no safety equipment, so weigh cost against duty and give a decision with reasons; pause: after the definition of stakeholder, and after the passage on duties to suppliers
sources: no

=== CH04 ===
title: Ways to Own a Business, and the Sole Proprietor
purpose: Show why the form of ownership matters, teach limited and unlimited liability, and explain the sole proprietorship with its strengths and limits.
pace: slow — liability is a new and abstract idea that later chapters depend on
style: descriptive
words: 4375
figures: 1
- fig01: two balance-style drawings of one business whose debts exceed its assets, one showing the shortfall falling on the owner's home and savings, the other stopping at the business
plate: a lone shopkeeper at a counter with scales, a ledger and shelves of jars, 1880s
sections:
4.1 | Why the Form of Ownership Matters | new idea | 775
4.2 | Sole Proprietorship | framework | 775
4.3 | Comparing the Forms | framework | 225
concepts:
- 4.1 | Liability, unlimited and limited, and who bears a business's losses | core | needs: risk, profit
- 4.1 | The main forms of ownership and the legal person | standard | needs: liability
- 4.2 | Sole proprietorship: meaning, features, strengths, limits and suitable fields | core | needs: liability
- 4.2 | Formation of a sole proprietorship and why it survives beside large businesses | standard | needs: sole proprietorship
- 4.3 | A first comparison of the forms on owner, money, risk and control | standard | needs: forms of ownership
defines:
- Liability | the duty to pay what the business owes, whether to a supplier, a lender or an employee
- Unlimited liability | the owner must pay all the business's debts, using personal property if the business cannot
- Limited liability | the owner can lose only the money put into the business, and personal property stays safe
- Legal person | an organisation that the law treats as separate from its owners, able to own property and make contracts
- Sole proprietorship | a business owned, financed and run by one person who keeps all profit and bears all loss
- Trade licence | official permission, given by a local authority, to carry on a particular business in a particular place
assumes: business, profit, risk, capital, supplier, location
words-in-use: none
case: Carried forward. Meghna and Sons is a sole proprietorship owned by Rafiq Uddin Mia, with a bank loan of Tk 60,000 taken on 1 March 2019. Position on 31 December 2019: assets Tk 400,000 (stock Tk 310,000 and other assets Tk 90,000); debts Tk 180,000 (owed to suppliers Tk 120,000 and to the bank Tk 60,000); the owner's own stake was therefore Tk 220,000 (400,000 - 180,000). The shop was closed for nine weeks in 2020. Position on 31 December 2020: assets Tk 380,000; debts Tk 430,000 (owed to suppliers Tk 370,000 and to the bank Tk 60,000); debts exceeded assets by Tk 50,000 (430,000 - 380,000). On 15 January 2021 Rafiq paid the Tk 50,000 shortfall from his personal savings. The shop's trade licence (illustrative number TL-2015-0417) was issued on 20 December 2014 and has been renewed each year.
history: The failure of the City of Glasgow Bank in 1878, when shareholders with unlimited liability lost their homes and savings. Search hint: City of Glasgow Bank 1878 collapse unlimited liability shareholders.
refs: Chapter 3, 'Social Responsibility of Business', section 3.2 'Responsibility to Society, Suppliers and Investors' — the lender and supplier whose claims the owner must meet; Chapter 5, 'Partnership', section 5.1 'The Idea and Types of Partnership' — what changes when two or more people share the business
need: Chapter 1, 'What Business Is, Does and Aims For', section 1.2 'What a Business Is'; Chapter 3, 'Social Responsibility of Business', section 3.2 'Responsibility to Society, Suppliers and Investors'
ladder: a lone street vendor who answers for everything (familiar); the bookshop's year-end position showing a shortfall (reshaped); a farmer who pledges land to buy seed (new setting); a one-person business weighing whether to share ownership as it grows (combined case)
practice: review: define liability and say how unlimited differs from limited liability, using one sum of your own; list four features of a sole proprietorship; give two fields where it suits and say why; explain why it survives beside large businesses; think: a tailor's assets are Tk 90,000 and her debts Tk 135,000, so say who must pay the gap under each kind of liability and what she might do; pause: after the definition of unlimited liability, and after the passage on the legal person
sources: no

=== CH05 ===
title: Partnership
purpose: Teach what a partnership is, the kinds of partnership and partner, the duties between partners, and how a partnership ends.
pace: standard — builds on liability and the sole proprietor; the new ideas arrive in small groups
style: descriptive
words: 4700
figures: 1
- fig01: how a year's profit is shared among three partners in the ratio of their capital, drawn as three hatched blocks with labels
plate: two clerks sharing a double desk in a counting-house with ledgers and a ship model, 1890s
sections:
5.1 | The Idea and Types of Partnership | new idea | 775
5.2 | Types of Partners and Their Duties | framework | 775
5.3 | Advantages, Disadvantages and Dissolution | framework | 550
concepts:
- 5.1 | Partnership, the partnership deed and the base on which it rests | core | needs: unlimited liability, sole proprietorship
- 5.1 | Kinds of partnership: by purpose and length, and by liability | standard | needs: partnership
- 5.2 | Active, sleeping and nominal partners, and the duties implied between partners | core | needs: partnership
- 5.2 | How profit and loss are shared when the deed is silent or specific | standard | needs: partnership deed, ratio (Appendix A1)
- 5.3 | Advantages and disadvantages of partnership, and how it differs from a sole proprietorship, ending with dissolution | core | needs: sole proprietorship, partnership
defines:
- Partnership | a business owned by two or more people who agree to run it together and share its profit
- Partner | one of the people who own a partnership and share in its profit, loss and duties
- Partnership deed | the written agreement that sets out how partners share capital, profit, work and decisions
- Partnership at will | a partnership with no fixed end date, which any partner can end by giving notice
- Active partner | a partner who takes a full part in running the business day to day
- Sleeping partner | a partner who puts in money and shares profit but takes no part in running the business
- Nominal partner | a person who lends their name to the business and takes no share, yet may still be answerable to outsiders
- Dissolution | the ending of the partnership between the partners, or of the whole business, with its affairs settled
assumes: sole proprietorship, liability, unlimited liability, capital, ratio
words-in-use: none
case: Carried forward. In 2020 Rafiq Uddin Mia met a Tk 50,000 shortfall from savings (Chapter 4). On 1 July 2021 Rafiq and his son Imran formed a partnership under a deed of that date. Capital: Rafiq Tk 400,000, Imran Tk 200,000, total Tk 600,000. Profit and loss are shared 2 : 1, the ratio of capital (400,000 : 200,000); both partners work full time. Profit for the year ended 30 June 2022 was Tk 360,000: Rafiq Tk 240,000 (360,000 x 2/3) and Imran Tk 120,000 (360,000 x 1/3). On 1 January 2023 Rafiq's second son Sohel joined as a sleeping partner with capital of Tk 200,000, taking total capital to Tk 800,000; profit is now shared 2 : 1 : 1. Profit for the year ended 31 December 2023 was Tk 480,000: Rafiq Tk 240,000 (480,000 x 2/4), Imran Tk 120,000 (480,000 x 1/4), Sohel Tk 120,000 (480,000 x 1/4). On 31 March 2024 the partners' capital, including profit left in the business, stood at Tk 1,200,000: Rafiq Tk 600,000, Imran Tk 300,000, Sohel Tk 300,000.
history: The partnership of Michael Marks and Thomas Spencer, formed in 1894 in Leeds, England, which grew into the retailer Marks and Spencer. Search hint: Marks and Spencer 1894 partnership Thomas Spencer.
refs: Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', section 4.1 'Why the Form of Ownership Matters' — liability, which partners share; Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares' — the next step when a partnership outgrows its form
need: Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', sections 4.1 'Why the Form of Ownership Matters' and 4.2 'Sole Proprietorship'
ladder: two friends splitting the cost and work of a tea stall (familiar); the bookshop's father-and-son deed (reshaped); a pair of fishers sharing a boat and net (new setting); a partnership with a sleeping partner facing a dispute and an exit (combined case)
practice: review: define partnership and name the base it rests on; compare active, sleeping and nominal partners; state three duties partners owe each other; list the ways a partnership can end; think: three partners put in Tk 300,000, Tk 200,000 and Tk 100,000 and earn Tk 180,000, so share the profit by capital and say what changes if the deed fixes equal shares; pause: after the passage on sleeping partners, and after profit sharing
sources: no

=== CH06 ===
title: Joint Stock Company
purpose: Teach the company as a separate legal person owned through shares, how private and public companies differ, how one is formed, and its merits and demerits.
pace: slow — shares, limited liability and the legal person arrive together and are abstract
style: descriptive
words: 5250
figures: 2
- fig01: the chain from shareholders to board of directors to managers, with arrows showing who elects and who reports
- fig02: the steps of forming a company in order, from agreeing the aims to receiving the certificate, drawn as numbered boxes
plate: a boardroom with directors around a long table beneath a company seal, 1880s
sections:
6.1 | The Company and Its Shares | new idea | 775
6.2 | Private and Public Companies | framework | 775
6.3 | Forming a Company and Issuing a Prospectus | technique | 550
6.4 | Merits and Demerits | framework | 550
concepts:
- 6.1 | The company as a legal person with limited liability | core | needs: legal person, limited liability
- 6.1 | Shares, shareholders and dividend | standard | needs: company
- 6.2 | Private and public companies compared | core | needs: company, shares
- 6.2 | Management by the board of directors | standard | needs: shareholders
- 6.3 | Steps of formation: the memorandum, the articles, incorporation, the prospectus and starting trade | core | needs: company, private and public company
- 6.4 | Merits and demerits of the company form, and whether it is the best form | core | needs: limited liability, partnership
defines:
- Company | a business that the law treats as a separate person, owned by shareholders through shares
- Share | one equal part of a company's capital, which gives its holder a part of ownership
- Shareholder | a person or organisation that owns one or more shares in a company
- Dividend | the part of a company's profit that is paid out to its shareholders
- Authorised capital | the largest amount of share capital that a company is permitted to raise under its rules
- Private company | a company that limits who may hold its shares and may not invite the public to buy them
- Public company | a company that may invite the public to buy its shares and whose shares can be freely traded
- Board of directors | the group chosen by shareholders to guide the company and appoint its senior managers
- Memorandum of association | the founding document that states a company's name, aims, home and capital
- Articles of association | the rules for running the company inside, including meetings, directors and shares
- Certificate of incorporation | the official paper that proves the company legally exists as a separate person
- Prospectus | the document by which a public company invites the public to buy its shares
- Certificate of commencement | the official paper that allows a public company to start business after it has raised enough money
assumes: legal person, limited liability, liability, partnership, sleeping partner, capital, ratio
words-in-use: share, stock
case: Carried forward. On 31 March 2024 the partners' capital was Tk 1,200,000: Rafiq Tk 600,000, Imran Tk 300,000, Sohel Tk 300,000 (Chapter 5). On 1 April 2024 the partners ended the partnership and formed Meghna and Sons Limited, a private company. Authorised capital Tk 2,000,000, divided into 200,000 shares of Tk 10 each. Shares issued 120,000 (120,000 x 10 = Tk 1,200,000): Rafiq 60,000, Imran 30,000, Sohel 30,000. Unissued shares 80,000 (Tk 800,000). Certificate of incorporation dated 15 April 2024. Directors: Rafiq (chairman), Imran (managing director), Sohel. For the year ended 31 March 2025 profit after all costs was Tk 540,000; the board proposed a dividend of Tk 2 a share, Tk 240,000 in all (120,000 x 2): Rafiq Tk 120,000, Imran Tk 60,000, Sohel Tk 60,000; the remaining Tk 300,000 was kept in the business. As a private company the business issued no prospectus.
history: The Dutch East India Company (VOC), chartered in 1602 in Amsterdam, whose shares could be bought and sold, and the English Joint Stock Companies Act of 1844 and Limited Liability Act of 1855. Search hint: Dutch East India Company 1602 first joint stock shares Amsterdam.
refs: Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', section 4.1 'Why the Form of Ownership Matters' — limited liability and the legal person; Chapter 9, 'The Share Market', section 9.1 'Shares and Their Kinds' — the kinds of shares and where they are traded
need: Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', section 4.1 'Why the Form of Ownership Matters'; Chapter 5, 'Partnership', section 5.3 'Advantages, Disadvantages and Dissolution'
ladder: a village pot of money shared among neighbours for a pump (familiar); the bookshop becoming a company (reshaped); a tea estate raising money from many small buyers (new setting); a company deciding whether to stay private or invite the public (combined case)
practice: review: define company and explain why it counts as a separate person; compare private and public companies on members, shares and the public offer; list the documents needed to form a company and say what each contains; state two merits and two demerits of the form; think: a company has 50,000 shares of Tk 10, earns Tk 80,000 profit and keeps half, so work out the dividend per share and the sum each holder of 5,000 shares receives; pause: after limited liability for shareholders, and after the memorandum and the articles
sources: yes

=== CH07 ===
title: Cooperative Societies
purpose: Teach what a cooperative society is, the principles it follows, the kinds found in Bangladesh, how it operates, and where it helps and falls short.
pace: standard — a self-contained form; new ideas arrive in small groups
style: descriptive
words: 4375
figures: 1
- fig01: members at the base voting in a general meeting, which elects a managing committee, which hires a manager; a second arrow shows surplus flowing back to members by their purchases
plate: villagers loading sacks onto a cart outside a cooperative store, 1870s
sections:
7.1 | The Idea and Principles of Cooperation | new idea | 775
7.2 | Types and Operation of Cooperatives | framework | 775
7.3 | Importance and Limits | framework | 225
concepts:
- 7.1 | The cooperative society, its aims and the principles it follows | core | needs: partnership, company
- 7.1 | Open membership and one member, one vote | standard | needs: cooperative society
- 7.2 | Kinds of cooperative found in Bangladesh, including those that help farmers market their crops | core | needs: cooperative society
- 7.2 | How a society is formed, financed, governed and shares its surplus | standard | needs: principles of cooperation
- 7.3 | The importance of cooperatives and their limits | standard | needs: kinds of cooperative
defines:
- Cooperative society | a business owned and run by its members, who join to meet a shared need rather than to earn the largest profit
- Open membership | the rule that anyone who meets the society's basic conditions may join, with no unfair barrier
- Democratic control | the rule that each member has one vote, however many shares or how much business they bring
- Surplus | the money left over after a cooperative pays its costs, which it shares or keeps for the members
- Patronage refund | a share of the surplus paid to members in proportion to the business they did with the society
- Credit cooperative | a society that collects savings from members and lends to them on fair terms
- Marketing cooperative | a society that gathers members' products, such as crops, and sells them for a better price
- Consumer cooperative | a society that buys goods in bulk and sells them to members at fair prices
- Producer cooperative | a society in which members make goods together and share the work and the reward
assumes: business, profit, partnership, company, share, shareholder, supplier
words-in-use: none
case: Case in this chapter is a members' purchasing society, an illustrative arrangement (membership rules differ by society and by law). On 3 February 2025 Meghna and Sons Limited joined the Dhaka Booksellers' Purchasing Society as one of 40 member shops. Each member holds one share of Tk 5,000, so share capital is Tk 200,000 (40 x 5,000). Each member has one vote. For the year ended 31 December 2025 the members bought books worth Tk 3,000,000 through the society. The society's surplus after costs was Tk 150,000. The general meeting voted to return 80% of the surplus to members as a patronage refund, Tk 120,000 (150,000 x 80/100), and to keep 20%, Tk 30,000, as a reserve. Meghna and Sons Limited bought books worth Tk 240,000 through the society, which is 8% of the total (240,000 / 3,000,000), so its refund was Tk 9,600 (120,000 x 8/100).
history: The Rochdale Society of Equitable Pioneers, opened in Rochdale, England, in December 1844 in Toad Lane, and the rules it set for its members. Search hint: Rochdale Pioneers 1844 Toad Lane principles.
refs: Chapter 5, 'Partnership', section 5.1 'The Idea and Types of Partnership' — a small group owning together; Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares' — the contrast of votes by member and votes by share
need: Chapter 5, 'Partnership', section 5.1 'The Idea and Types of Partnership'; Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares'
ladder: neighbours buying rice together to get a lower price (familiar); the bookshops' purchasing society (reshaped); dairy farmers pooling milk for sale to a city (new setting); a society deciding how to use its surplus when members disagree (combined case)
practice: review: define cooperative society and give three of its principles; explain why one member has one vote and how that differs from a company; name four kinds of cooperative and say who each helps; describe how a surplus is shared; think: a farmers' society sells its crop for Tk 600,000 against Tk 520,000 if each farmer sold alone and has 40 members, so find the gain per member and say what the members might do with a surplus; pause: after the principles, and after the passage on sharing surplus
sources: yes

=== CH08 ===
title: State Enterprise
purpose: Teach what a state enterprise is, why governments run businesses, the forms they take, and why many struggle to make a profit.
pace: standard — builds on ownership forms already met; one new idea at a time
style: descriptive
words: 4375
figures: 1
- fig01: a tree with state enterprise at the top and three branches: run as a government office, set up as a public corporation, formed as a government-owned company
plate: a municipal waterworks pumping engine hall with an engineer at the controls, 1880s
sections:
8.1 | Meaning, Need and Importance | new idea | 775
8.2 | Forms of State Enterprise | framework | 775
8.3 | Performance and Reform | framework | 225
concepts:
- 8.1 | The state enterprise, the public sector and the reasons governments run businesses, including the fields where it fits | core | needs: business, company
- 8.1 | Nationalisation, monopoly and the case for and against state ownership | standard | needs: state enterprise
- 8.2 | Departmental undertaking, public corporation and government company compared | core | needs: legal person, company
- 8.2 | Public utilities and joint ventures with private businesses | standard | needs: forms of state enterprise
- 8.3 | Why state enterprises often lose money, and the remedies tried, including privatisation | standard | needs: forms of state enterprise
defines:
- State enterprise | a business owned and run by the government, set up to serve the public or to earn money for the state
- Public sector | all the businesses and organisations that the government owns or controls
- Nationalisation | the act of a government taking over a privately owned business and making it state property
- Monopoly | a market in which only one seller supplies a good or service, so customers have no choice
- Departmental undertaking | a state business run as a part of a government office and funded from its budget
- Public corporation | a state business set up by a special law, with its own legal identity and some freedom to act
- Government company | a company, formed under company law, in which the government owns most or all of the shares
- Public utility | a service that everyone needs and that is hard to supply through competition, such as water or electricity
- Privatisation | the sale or handing over of a state enterprise to private owners
assumes: business, company, share, legal person, profit, limited liability, supplier
words-in-use: none
case: none
history: The British Broadcasting Corporation, set up as a company in 1922 and made a public corporation under a Royal Charter on 1 January 1927. Search hint: BBC royal charter 1927 public corporation Reith.
refs: Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares' — a government company is a company in law; Chapter 7, 'Cooperative Societies', section 7.1 'The Idea and Principles of Cooperation' — another form that does not exist only for private profit
need: Chapter 4, 'Ways to Own a Business, and the Sole Proprietor', section 4.1 'Why the Form of Ownership Matters'; Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares'
ladder: a village committee that runs a shared well (familiar); a city bus service run by the city (reshaped); a national railway or power supplier (new setting); a government deciding whether to keep, reform or sell a loss-making mill (combined case)
practice: review: define state enterprise and name two reasons a government runs a business; compare the three forms on control, money and legal identity; explain what a public utility is and why it is often state-run; give two causes of loss in state enterprises and one remedy; think: a government mill loses Tk 40 crore a year while employing 3,000 people, so set out the case for keeping it, the case for selling it, and a decision; pause: after the three forms are introduced, and after the causes of loss
sources: no

=== CH09 ===
title: The Share Market
purpose: Teach the kinds of shares, how a company first offers shares to the public, and how stock exchanges, including the Dhaka Stock Exchange, let investors trade them.
pace: standard — builds on shares from Chapter 6; the new ideas are the market and its parts
style: descriptive
words: 4375
figures: 1
- fig01: companies selling shares to investors in the primary market (left), and investors trading among themselves through brokers on the stock exchange in the secondary market (right)
plate: a stock exchange floor with brokers and a large chalk board, 1880s
sections:
9.1 | Shares and Their Kinds | new idea | 775
9.2 | The Initial Public Offering | technique | 225
9.3 | Stock Exchanges and the Dhaka Stock Exchange | framework | 775
concepts:
- 9.1 | Ordinary and preference shares, and which kind suits which investor | core | needs: share, dividend
- 9.1 | The share market, with its primary and secondary parts | standard | needs: share, investor
- 9.2 | The initial public offering and the steps that lead to it | standard | needs: prospectus, public company
- 9.3 | The stock exchange and the functions of the Dhaka Stock Exchange | core | needs: secondary market, public company
- 9.3 | Brokers, share price indices and the regulator's role | standard | needs: stock exchange
defines:
- Ordinary share | a share whose holder votes at meetings and receives a dividend that rises and falls with the company's profit
- Preference share | a share whose holder is paid a fixed dividend before ordinary shareholders but usually has no vote
- Share market | the whole system of buying and selling shares, both when they are first issued and afterwards
- Primary market | the part of the share market where a company sells new shares directly to investors for the first time
- Secondary market | the part of the share market where investors buy and sell shares that already exist
- Initial public offering | the first time a company invites the public to buy its shares
- Stock exchange | an organised market with rules where approved members trade company shares and other securities
- Broker | a licensed person or firm that buys and sells shares for clients and earns a fee
- Share price index | a single number that shows how the prices of a chosen group of shares have moved together
assumes: share, shareholder, dividend, company, public company, private company, prospectus, authorised capital, investor, capital, board of directors
words-in-use: stock
case: Carried forward. Meghna and Sons Limited has 120,000 issued shares of Tk 10 and an authorised capital of Tk 2,000,000 (200,000 shares); Rafiq, Imran and Sohel hold 60,000, 30,000 and 30,000 shares. At a board meeting on 10 February 2026 the directors considered raising Tk 4,000,000 for a second shop through an initial public offering of 400,000 new shares at Tk 10 each (400,000 x 10). The offering would need authorised capital to rise to at least 520,000 shares (120,000 + 400,000), Tk 5,200,000, and the company to become a public company. After the offering the three founders' 120,000 shares would be 23.1% of 520,000 shares (120,000 / 520,000) and outside investors would hold 76.9%. The board noted the cost of the offering and the loss of control, and deferred the decision. Imran Rafiq was asked to prepare a cost estimate by 31 March 2026.
history: The Buttonwood Agreement signed by 24 brokers in New York on 17 May 1792, which began the organised trading that became the New York Stock Exchange. Search hint: Buttonwood Agreement 1792 New York brokers.
refs: Chapter 6, 'Joint Stock Company', section 6.3 'Forming a Company and Issuing a Prospectus' — the prospectus a public company issues; Chapter 12, 'Institutions and Business Combination', section 12.1 'Institutions That Promote Business' — the regulator of the share market
need: Chapter 6, 'Joint Stock Company', sections 6.1 'The Company and Its Shares', 6.2 'Private and Public Companies' and 6.3 'Forming a Company and Issuing a Prospectus'
ladder: neighbours selling their shares in a village pump fund to each other (familiar); the bookshop company weighing a public offer (reshaped); a tea estate listing its shares (new setting); an investor choosing between an ordinary and a preference share for a retirement fund (combined case)
practice: review: tell ordinary from preference shares on vote, dividend and risk; separate the primary from the secondary market with an example of each; describe the steps by which a company offers shares to the public; list the main functions of a stock exchange; think: an investor has Tk 100,000, wants steady income and dislikes risk, so choose between the two kinds of share and explain; pause: after the two kinds of share, and after the split between the primary and secondary markets
sources: no

=== CH10 ===
title: Foreign Trade: Measuring It and Doing It
purpose: Explain why nations trade, how trade between nations is measured, and how an export or import is carried out, with the documents and barriers involved.
pace: slow — comparative advantage and the two balances are new and abstract, and the chapter mixes ideas with arithmetic
style: mixed
words: 5150
figures: 2
- fig01: the steps of an export in order, from enquiry and order through letter of credit and shipment to payment, drawn as numbered boxes
- fig02: two hatched columns, exports and imports, with the gap between them labelled as the balance of trade
plate: a quay with cranes loading crates onto a sailing ship, a customs officer beside the gangway, 1870s
sections:
10.1 | Why Nations Trade, and Why It Matters | new idea | 775
10.2 | Measuring Trade Between Nations | technique | 775
10.3 | Export and Import Procedure and Documents | technique | 775
10.4 | Barriers to Export Trade | framework | 225
concepts:
- 10.1 | Why nations trade: differences in resources and comparative advantage | core | needs: exchange, factors of production
- 10.1 | The importance of foreign trade to a country such as Bangladesh | standard | needs: foreign trade
- 10.2 | Visible and invisible trade, the balance of trade and the balance of payments | core | needs: export, import
- 10.2 | Reading a surplus or a deficit | standard | needs: balance of trade, percentage (Appendix A1)
- 10.3 | The export and import procedure from first enquiry to payment and customs clearance | core | needs: foreign trade, supplier
- 10.3 | The main documents in foreign trade, including the bill of lading and the charter party | standard | needs: export and import procedure
- 10.4 | Barriers to export trade in Bangladesh, and tariff and non-tariff barriers | standard | needs: export
defines:
- Foreign trade | the buying and selling of goods and services between people or businesses in different countries
- Export | a good or service sold to a buyer in another country
- Import | a good or service bought from a seller in another country
- Comparative advantage | a country's ability to make a good at a lower sacrifice of other goods than another country can
- Visible trade | trade in goods that can be seen and counted at a port, such as books, cloth and machines
- Invisible trade | trade in services, such as shipping, insurance and tourism, that cannot be seen at a port
- Balance of trade | the value of a country's visible exports minus the value of its visible imports
- Balance of payments | the full record of money flowing into and out of a country over a period for all kinds of dealings
- Letter of credit | a bank's written promise to pay the exporter once agreed documents are shown
- Bill of lading | a receipt and contract issued by a shipping company for goods it has accepted for carriage
- Charter party | the contract by which the owner of a ship hires the whole ship, or part of it, to another business
- Customs duty | a tax charged on goods when they cross a national border
- Non-tariff barrier | a rule or practice other than a tax that makes it harder to trade, such as a quota or a quality test
assumes: exchange, factors of production, supplier, good, service, trade, business, profit, percentage, ratio
words-in-use: balance, goods
case: Carried forward. Meghna and Sons Limited is a company (since 1 April 2024). The figures here use an assumed rate of Tk 120 for one US dollar, chosen only for this illustration. Import: on 3 March 2025 the company opened a letter of credit for 1,500 English-language books from a publisher in the United Kingdom, invoice value US$ 6,000 (Tk 720,000: 6,000 x 120). The goods were shipped on 28 March 2025 under a bill of lading of that date and reached Chattogram on 29 April 2025. Customs duty and taxes were Tk 108,000 (15% of 720,000) and the bank's charges on the letter of credit were Tk 7,200 (1% of 720,000). Landed cost Tk 835,200 (720,000 + 108,000 + 7,200), which is Tk 556.80 a book (835,200 / 1,500). Export: in 2025 the company also sold 200 Bangla books to a bookseller in London, invoice value US$ 2,000 (Tk 240,000: 2,000 x 120). Balance of trade for the company's goods: 240,000 - 720,000 = minus Tk 480,000, a deficit. Invisible trade: marine insurance paid to a foreign insurer US$ 150 (Tk 18,000: 150 x 120), so goods and services together show a deficit of Tk 498,000 (480,000 + 18,000).
history: David Ricardo's example of cloth and wine traded between England and Portugal in On the Principles of Political Economy and Taxation, 1817. Search hint: Ricardo 1817 comparative advantage wine cloth Portugal.
refs: Chapter 11, 'Multinational Corporations', section 11.1 'What a Multinational Corporation Is' — firms that operate in several countries; Chapter 12, 'Institutions and Business Combination', section 12.2 'Zones, Export Bodies and Others' — bodies that help exporters
need: Chapter 1, 'What Business Is, Does and Aims For', section 1.3 'Trade, Commerce and Industry'; Chapter 2, 'Resources, Location and Environment', section 2.1 'The Factors of Production'
ladder: two neighbours, one good at growing rice and one at weaving, trading with clean numbers (familiar); the bookshop's import and export with messier figures (reshaped); a country selling garments and buying machinery (new setting); a country weighing a rising deficit against its need for imported fuel (combined case)
practice: review: explain comparative advantage with a pair of goods of your own; separate visible from invisible trade with two examples of each; list the steps of an export in order; name five documents used in foreign trade and say what each does; calculate: a country sells goods worth 48 billion and buys goods worth 61 billion, so find the balance of trade and say if it is a surplus or deficit; think: a country has a deficit in goods but earns much from workers abroad, so say what the balance of payments might show and why; pause: after comparative advantage, and after the worked deficit
sources: yes

=== CH11 ===
title: Multinational Corporations
purpose: Teach what a multinational corporation is, why firms become multinational, the three groups of staff such firms use, and the gains and problems for the countries that host them.
pace: standard — builds on foreign trade; one new idea at a time
style: descriptive
words: 4375
figures: 1
- fig01: a parent company in its home country with a subsidiary in a host country, and three groups of staff labelled by their country of origin
plate: a large works with chimneys beside a railway and a steamship in dock, 1880s
sections:
11.1 | What a Multinational Corporation Is | new idea | 775
11.2 | People in a Multinational | framework | 225
11.3 | Why Multinationals Matter, and Their Problems | framework | 775
concepts:
- 11.1 | The multinational corporation and the reasons firms set up in other countries | core | needs: company, foreign trade
- 11.1 | Home country, host country and subsidiary | standard | needs: multinational corporation
- 11.2 | Parent-country, host-country and third-country nationals in a multinational's staff | standard | needs: home country, host country
- 11.3 | The gains a multinational brings to a host country and the problems it can cause | core | needs: host country, technology transfer
- 11.3 | Technology transfer and the way a country such as Bangladesh deals with multinationals | standard | needs: host country
defines:
- Multinational corporation | a company that owns and runs business operations in two or more countries
- Home country | the country where a multinational has its headquarters and where its parent company is based
- Host country | a country in which a multinational sets up a branch or subsidiary and operates
- Subsidiary | a company that is owned or controlled by another, larger company called the parent
- Parent-country national | an employee of a multinational who comes from the country of its headquarters
- Host-country national | an employee of a multinational who comes from the country where it is operating
- Third-country national | an employee of a multinational who comes from neither its home nor its host country
- Technology transfer | the passing of knowledge, machines and methods from one country or firm to another
assumes: company, foreign trade, export, import, investor, subsidiary, shareholder
words-in-use: none
case: Case in this chapter is an illustrative multinational. Northwind Stationery plc (fictional) is headquartered in the United Kingdom and began operating through a subsidiary in Dhaka, Northwind Stationery Bangladesh Limited, on 5 May 2024. The parent invested US$ 1,000,000, Tk 120,000,000 at the illustration's assumed rate of Tk 120 a dollar (1,000,000 x 120). The subsidiary has 90 staff: 3 parent-country nationals from the United Kingdom, 2 third-country nationals from India, and 85 host-country nationals from Bangladesh (3 + 2 + 85 = 90). Host-country nationals are 94.4% of staff (85 / 90). From 1 September 2025 Meghna and Sons Limited has sold Northwind notebooks, and its purchases from the subsidiary between 1 September and 31 December 2025 were Tk 180,000.
history: The Singer Manufacturing Company's factory at Kilbowie, near Glasgow, Scotland, opened in 1867 as one of the first overseas factories of an American firm. Search hint: Singer Kilbowie factory 1867 Scotland first overseas.
refs: Chapter 10, 'Foreign Trade: Measuring It and Doing It', section 10.1 'Why Nations Trade, and Why It Matters' — the gains from trade that multinationals extend; Chapter 12, 'Institutions and Business Combination', section 12.2 'Zones, Export Bodies and Others' — zones that attract overseas investors
need: Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares'; Chapter 10, 'Foreign Trade: Measuring It and Doing It', section 10.1 'Why Nations Trade, and Why It Matters'
ladder: a village shop that opens a second branch in a neighbouring village (familiar); a stationery brand with a subsidiary in Dhaka (reshaped); a foreign mobile network entering a small country (new setting); a government deciding how much to welcome a large overseas investor (combined case)
practice: review: define multinational corporation and name three reasons a firm becomes one; tell home country from host country with an example; explain the three groups of staff and why a multinational mixes them; list two gains and two problems for a host country; think: a foreign factory will employ 400 local workers and train them, but may send most of its profit abroad and push local makers out, so weigh both sides and say what rules a government might set; pause: after the three groups of staff, and after the gains and problems
sources: no

=== CH12 ===
title: Institutions and Business Combination
purpose: Teach the bodies that promote and regulate business in Bangladesh, and why and how businesses combine, with the opportunities and threats of combining.
pace: standard — two related topics, each in small groups
style: descriptive
words: 4925
figures: 1
- fig01: two drawings side by side: horizontal combination (three shops of the same kind joined) and vertical combination (a printer, a wholesaler and a shop joined along one chain)
plate: merchants meeting in a chamber hall with a model of a harbour on a table, 1890s
sections:
12.1 | Institutions That Promote Business | framework | 775
12.2 | Zones, Export Bodies and Others | framework | 450
12.3 | Forms of Business Combination | framework | 550
12.4 | Opportunities and Threats | framework | 550
concepts:
- 12.1 | The role of bodies that promote and regulate business, including the securities regulator | core | needs: stock exchange, state enterprise
- 12.1 | Chambers of commerce and the national federation of chambers | standard | needs: business
- 12.2 | Export processing zones and the authority that runs them | standard | needs: export, foreign trade
- 12.2 | The export promotion body, the trade corporation and other support bodies (the writer confirms each body's full name and role) | standard | needs: export, foreign trade
- 12.3 | Forms of combination: cartel, holding company, merger and the directions of integration | core | needs: company, share
- 12.4 | Why businesses combine, and the opportunities and threats that follow | core | needs: forms of combination
defines:
- Securities regulator | a public body that makes and enforces rules for the share market in order to protect investors
- Chamber of commerce | an association of local businesses that speaks for them and helps them trade
- Export processing zone | a designated area with special facilities and incentives, set up to attract factories that make goods for export
- Business combination | two or more businesses joining together, by agreement or by one taking over another, to act as a larger unit
- Cartel | a loose agreement among businesses that stay separate but fix prices or output together
- Holding company | a company that controls others by owning enough of their shares
- Merger | the joining of two or more businesses into one, with the owners of each becoming owners of the new business
- Horizontal integration | joining businesses that sell the same kind of good or service at the same stage of the chain
- Vertical integration | joining businesses at different stages of the chain, such as a printer, a wholesaler and a shop
assumes: stock exchange, share, company, export, foreign trade, state enterprise, subsidiary, investor, business, supplier
words-in-use: none
case: Carried forward. Meghna and Sons Limited has been a member since 1 July 2022 of a district traders' chamber that belongs to a national federation of chambers (illustrative), with an annual subscription of Tk 12,000. Sales for the year ended 31 March 2026 were Tk 3,600,000. On 12 May 2026 the board considered buying a printing press for Tk 2,500,000 (vertical integration) and rejected it. On 1 June 2026 the company took over Shapla Books, a shop with annual sales of Tk 1,800,000, for Tk 900,000, paid by a bank loan of Tk 500,000 and retained profit of Tk 400,000 (500,000 + 400,000 = 900,000). Shapla Books ceased to exist as a separate firm. Combined annual sales of the two shops are Tk 5,400,000 (3,600,000 + 1,800,000), and Shapla Books' sales are one third of the combined figure.
history: The Standard Oil Trust of 1882 in the United States, the Sherman Antitrust Act of 1890, and the order of 1911 that broke the company into parts. Search hint: Standard Oil trust 1882 Sherman Act 1890 breakup 1911.
refs: Chapter 9, 'The Share Market', section 9.3 'Stock Exchanges and the Dhaka Stock Exchange' — the market the securities regulator oversees; Chapter 10, 'Foreign Trade: Measuring It and Doing It', section 10.4 'Barriers to Export Trade' — the barriers these bodies help exporters overcome; Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares' — a holding company is a company that owns shares in others
need: Chapter 6, 'Joint Stock Company', section 6.1 'The Company and Its Shares'; Chapter 9, 'The Share Market', section 9.3 'Stock Exchanges and the Dhaka Stock Exchange'
ladder: two neighbouring tea stalls agreeing to share a supplier (familiar); the bookshop company taking over a smaller shop (reshaped); two airlines or two banks joining (new setting); a group deciding between a cartel, a merger and staying separate when a large rival arrives (combined case)
practice: review: say what a chamber of commerce does for its members; describe the purpose of an export processing zone; compare a cartel, a holding company and a merger; tell horizontal from vertical integration with an example of each; think: three bakeries each earning Tk 60,000 a month consider joining, so list two opportunities and two threats and decide whether to merge or only cooperate; pause: after the securities regulator, and after the forms of combination
sources: no

=== A1 ===
title: Maths You Will Use
purpose: Give a short reference to the arithmetic used in the book: percentages, change, ratios, averages, rearranging an equation, rounding and reading a graph.
pace: standard — a reference page, not a lesson
style: calculation
words: 1000
figures: 0
sections:
A1.1 | Percentages and percentage change | reference | 250
A1.2 | Ratios and averages | reference | 250
A1.3 | Rearranging an equation and rounding | reference | 250
A1.4 | Reading a graph | reference | 250
concepts:
- A1.1 | Percentage, and percentage change | standard | needs: none
- A1.2 | Ratio and average | standard | needs: none
- A1.3 | Rearranging a formula to find a missing value, and rounding sensibly | standard | needs: none
- A1.4 | Reading the axes and points of a simple graph | standard | needs: none
defines:
- Percentage | a part of a whole written out of one hundred, so that 15 percent means 15 out of every 100
- Ratio | a way to compare two or more amounts by showing how many times each fits into a common unit
- Average | the total of a set of numbers divided by how many numbers there are
assumes: none
words-in-use: none
case: none
history: none
refs: Chapter 2, 'Resources, Location and Environment', section 2.3 'The Business Environment' — a fall in sales expressed as a percentage; Chapter 5, 'Partnership', section 5.2 'Types of Partners and Their Duties' — profit shared by ratio; Chapter 10, 'Foreign Trade: Measuring It and Doing It', section 10.2 'Measuring Trade Between Nations' — figures in balances
need: nothing
ladder: one clean example for each topic, then one with a messier figure, then a short note on common slips
practice: review: none (a reference, not a lesson)
sources: no
