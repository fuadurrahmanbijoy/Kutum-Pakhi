# Signature Printing: Accepted Theory

## Terms
- **Sheet**: one physical A4 paper, landscape. Two sides (front, back), two book pages per side, so **4 book pages per sheet**.
- **Signature**: a group of *k* sheets, nested and folded in half together. It holds **4k book pages**.
- **Book page**: one A4 portrait page of the source PDF, shrunk to ~70% to fit two side by side.

## Layout of one sheet (pages numbered 1..P inside a signature, P = 4k)
For sheet *i* (0 = outermost):

| Side  | Left    | Right   |
|-------|---------|---------|
| Front | P - 2i  | 1 + 2i  |
| Back  | 2 + 2i  | P-1-2i  |

Example, one sheet (P = 4): front is 4 | 1, back is 2 | 3. Page 2 sits behind page 1, page 3 behind page 4.

## Flip and turns
- The pile is flipped **like a book** (around the vertical edge). Left and right swap, top stays top, so **no 180° rotation** is needed.
- Printers take paper from the top of the stack, so sheet 1 prints first. Flipping the whole pile like a book brings sheet 1 back on top, so the **backs use the same sheet order as the fronts**.
- **WYSIWYG**: each output page is exactly what you see on screen, the top of the screen being the top of the landscape sheet.
- Two safety switches exist (rotate backs 180°, reverse back order), **off by default**, for printers that behave differently. A test print confirms the setup.

## Leftovers
- Sheets needed = ceil(pages / 4). Missing pages become **blank pages at the end**.
- If sheets don't divide evenly by *k*, the user chooses: **smaller last signature** (6,6,4), **merge extras into the previous one** (6,8), or **pad to a full signature**.

## Fidelity
- Original pages are embedded as vector pages (never rasterized), so **fonts and sharpness stay identical**.
- **Color mode**: the cream background is sampled from the source and fills the whole sheet, including margins and blanks. **B/W mode**: plain white.
- Margin is near zero by default and tucked in advanced settings.

## Workflow
Print fronts, re-insert the same pile, print backs, then split the pile into sub-piles of *k* sheets, fold each, and bind.
