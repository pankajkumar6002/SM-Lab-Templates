---
# =====================================================================
#  MARP TEMPLATE : matches the NISER/SMLab Beamer deck
# =====================================================================
#  HOW TO USE
#   1. Put this file in a folder with a media/ subfolder containing
#      dae_logo.svg, hbni_logo.png, niser_logo_blue.svg and
#      smlab_logo.svg (the logos used on the title slide).
#   2. Open it in VS Code with the "Marp for VS Code" extension and
#      click the preview icon. Or use the command line:
#         marp marp_template.md --html            (make a web page)
#         marp marp_template.md --pdf --html      (make a PDF)
#         marp marp_template.md --pptx --html     (make a PowerPoint)
#   3. Edit only the parts marked  >>> EDIT <<<  to get started.
#
#  DESIGN NOTE (delete this block once you've read it)
#   The old version of this template used the generic "AI slide deck"
#   formula: a solid color bar across the top AND bottom of every
#   slide, plus rounded, drop-shadowed boxes for callouts. That's the
#   same visual pattern every Marp starter kit defaults to, so it
#   reads as templated no matter what colors you put in it.
#   This version instead uses ONE structural idea, used nowhere else
#   in the deck: a solid vertical "spine" down the left edge (like
#   the bound edge of a lab notebook). It's purely decorative : your
#   name, the short title, and the page number sit in a quiet footer
#   line at the bottom of each slide instead, the more usual spot.
#   Everything else : headings, tables, callouts : is
#   built from thin rules instead of filled, shadowed boxes. Colors
#   are used as accents (a rule, a border), not as backgrounds, so
#   nothing fights the navy spine for attention.
#   The fonts are deliberate too: Kreon (a rounded serif with a warm,
#   book-like feel) for headings, paired with Helvetica (a plain,
#   neutral sans-serif) for body text : a nod to this being a
#   research/lab deck rather than a marketing deck.
#
#  ABOUT COMMENTS
#   - Inside this top block (between the two --- lines), a line that
#     starts with # is a comment. Never put a comment on the SAME
#     line as a setting (e.g. "paginate: true # comment") : Marp
#     reads the comment as part of the value and silently breaks.
#   - Inside the CSS block, comments look like /* comment */
#   - In the slides below, comments look like [//]: # (comment)
#     Do NOT use <!-- comment --> for notes to yourself: Marp turns
#     those into SPEAKER NOTES that can show up in exports.
# =====================================================================

marp: true

# ---- BASIC SETTINGS -------------------------------------------------
#  IMPORTANT: never put a comment on the same line as a setting.

# Built-in themes: default | gaia | uncover
theme: default

# true = show page numbers, false = hide them
paginate: true

# 16:9 = widescreen, 4:3 = old square-ish screens
size: 16:9

# katex lets you write formulas like $E = mc^2$
math: katex

# Language of the document
lang: en

# ---- INFO ABOUT THE FILE (shown in the browser tab / PDF info) ------
#  >>> EDIT <<<
title: Your Presentation Title
author: Your Full Name
description: A short description of this presentation

# ---- FOOTER  >>> EDIT <<<
#  Shown at the bottom of every slide: your name and a short title on
#  the left, the page number on the right. Marp only gives you one
#  footer field, so name and short title are combined into one line
#  here - separate them with the same "·" shown below, or your own
#  short title with " - " between them, whatever you prefer.
footer: 'Your Full Name &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;Your Presentation Title'

# ---- HEADER (optional) ----------------------------------------------
#  Text at the top of every slide, ABOVE the content area (not part
#  of the spine). Most decks don't need this. Remove the # to use it.
# header: 'Your Institute'

# =====================================================================
#  CSS  (the design of your slides)  >>> EDIT <<<
#  Change the values in the first block to restyle everything.
# =====================================================================
style: |
  @import url('https://fonts.googleapis.com/css2?family=Kreon:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap');

  /* ---------- 1. COLORS: change these first ----------
     These match the finalized Beamer deck exactly, so both decks
     stay on-brand. Edit MainColor's value here AND in the .tex file
     if you ever change it, since the two files don't share colors
     automatically. */
  section {
    --ink:    #1c3c6b;   /* MainColor: navy - spine, headings, ink   */
    --signal: #FF3333;   /* AccentColor: red - thin accents only     */
    --good:   #0a1696d7;   /* GoodColor: muted teal-green               */
    --paper:  #F6F5F1;   /* LightGrey: warm off-white - slide bg      */

    /* ---- SPINE ON/OFF -------------------------------------------
       --spine-w is the width of the left-edge navy strip. To remove
       it from every slide, change the line below to:
           --spine-w: 0px;
       That's it - the strip disappears and the left margin matches
       the other three sides. Change it back to 72px any time to
       bring it back. */
    --spine-w: 0px;      /* width of the left-edge spine             */
    --gap: 56px;          /* space between the spine and your text    */

    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    font-size: 27px;
    color: var(--ink);
    /* The spine is a sharp two-color fade on the slide's OWN
       background, not a separate shape drawn on top. (An earlier
       version tried to draw it as a separate shape, and it quietly
       failed to show up when Marp turned the slide into a picture -
       this way works reliably everywhere.) */
    background: linear-gradient(to right,
      var(--ink) 0, var(--ink) var(--spine-w),
      var(--paper) var(--spine-w), var(--paper) 100%);
    position: relative;
    padding: 56px 64px 62px calc(var(--spine-w) + var(--gap));
    align-content: start;  /* content starts at the top, not centered */
  }

  /* ---------- 2. FOOTER (name, short title, page number) ----------
     The spine is purely decorative - this is what actually shows
     your name, short title and page number, in the usual spot: a
     quiet line at the bottom of the slide, not inside the spine. */
  section footer {
    position: absolute;
    left: calc(var(--spine-w) + var(--gap));
    right: 130px;
    bottom: 20px;
    text-align: left;
    color: rgba(0, 0, 0, 0.8);
    font-size: 0.45em;
    letter-spacing: 0.01em;
  }
  section[data-marpit-pagination]::after {
    content: attr(data-marpit-pagination);
    position: absolute;
    right: 64px;
    bottom: 20px;
    text-align: right;
    color: rgba(21,42,74,0.6);
    font-size: 0.45em;
    background: none;
  }
  section:not([data-marpit-pagination])::after { content: none; }

  /* ---------- 3. HEADINGS ----------
     A thin rule sized to the text, not a full-wid   th colored bar. */
  section h1 {
    font-family: 'Kreon', serif;
    font-weight: 600;
    font-size: 1.65em;
    color: var(--ink);
    display: inline-block;
    border-bottom: 2px solid var(--signal);
    padding-bottom: 0.15em;
    margin: 0 0 0.7em 0;
  }
  section h2 { font-family: 'Kreon', serif; font-weight: 600; color: var(--ink); }
  section h3 { font-family: 'Kreon', serif; font-weight: 500; font-style: italic; color: var(--ink); }
  section strong { color: var(--ink); }
  section a { color: var(--good); }
  section li::marker { color: var(--signal); }

  /* ---------- 4. TITLE SLIDE ----------
     The title and subtitle sit in a solid navy band (no rounded
     corners, no drop shadow - that's what made the old version read
     as generic). Everything on this slide is centered. */
  section.title {
    padding-top: 90px;
    text-align: center;
  }
  section.title h1 {
    display: block;
    width: 100%;
    box-sizing: border-box;
    background: var(--ink);
    color: #ffffff;
    border: none;
    font-size: 1.9em;
    margin: 0;
    padding: 0.55em 0.75em 0.12em;
  }
  section.title h3 {
    display: block;
    width: 100%;
    box-sizing: border-box;
    background: var(--ink);
    color: rgba(255,255,255,0.75);
    font-style: normal;
    font-weight: 400;
    font-size: 1em;
    margin: 0 0 0.9em 0;
    padding: 0 0.75em 0.6em;
  }
  section.title .presented-by { font-size: 0.85em; color: var(--ink); margin: 0; }
  section.title .name { font-family: 'Kreon', serif; font-weight: 600; font-size: 1.3em; margin: 0.1em 0 0; }
  section.title .meta { color: #4a5a72; margin: 0.2em 0 0; }

  /* Logos: plain images with a thin line between them, like the top
     of formal letter paper - not boxed, not shadowed. Wrapped in a
     <span class="logos"> on the title slide below (raw HTML, so it
     needs --html - already required by the presented-by/name/meta
     lines on that slide, so nothing new to turn on).
     Size: every logo is scaled to the same HEIGHT (--logo-h) so a
     row of different logos lines up neatly; --logo-max-w stops any
     single very wide logo from dominating the row. object-fit:
     contain keeps each logo's own proportions - nothing gets
     stretched or squashed.
     Want ONE particular logo a different size than the rest? Add a
     style straight on that <img> tag, e.g.:
       <img src="./media/dae_logo.svg" alt="DAE" style="height:60px">
     which overrides --logo-h for just that image. */
  .logos {
    --logo-h: 250px;      /* height every logo is scaled to   */
    --logo-max-w: 150px; /* widest any single logo can get   */
  }
  .logos img {
    height: var(--logo-h);
    width: auto;
    max-width: var(--logo-max-w);
    object-fit: contain;
    vertical-align: middle;
    margin-right: 100px;
    padding-right: 100px;
    border-right: 0px solid rgba(21,42,74,0.25);
  }
  .logos img:last-child { border-right: none; margin-right: 0; padding-right: 0; }

   /* ---------- 5. TWO COLUMNS ----------
     Two independent side-by-side boxes, laid out with CSS Grid —
     not the browser's automatic "flow text into 2 columns" mode.
     That's a deliberate choice: with automatic columns, forcing
     "Right side" to start a new column can leave it sitting a few
     pixels higher or lower than "Left side", because the browser's
     column-balancing math doesn't guarantee the two starting points
     line up. Grid rows always line up exactly, so this doesn't
     happen. See the markdown below for how each side is written:
     each one is just wrapped in its own <div>. */
  section.cols {
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 48px;
  }
  section.cols h1 { grid-column: 1 / -1; justify-self: start; }
  section.cols h3 { border-left: 2px solid rgba(21,42,74,0.25); padding-left: 0.5em; margin-top: 0; }

  /* ---------- 6. CALLOUTS ----------
     A left border only - no fill, no shadow, no rounded corners.
     Reads like a note in the margin of a book, not a colored box
     from an app. */
  section blockquote {
    border-left: 3px solid var(--ink);
    background: none;
    margin: 0.6em 0;
    padding: 0.2em 0 0.2em 1em;
    font-style: normal;
    color: var(--ink);
  }
  section blockquote::before, section blockquote::after { content: none; }

  /* Optional 3-color callouts (Note / Warning / Good) for the one
     slide that shows all three side by side. Needs --html (see that
     slide's comment). */
  .callout { border-left: 3px solid var(--ink); padding: 0.35em 0 0.35em 1em; margin: 0.5em 0; }
  .callout.warn { border-color: var(--signal); }
  .callout.good { border-color: var(--good); }
  .callout b { display: block; font-family: 'Kreon', serif; font-style: italic; }

  /* ---------- 7. TABLE (matches the clean-line table style in the .tex deck) ----------
     NOTE: these rules say "table th" / "table td", not just "th" /
     "td" on their own. Marp already has its own table style written
     the same exact way, and a shorter, plainer rule doesn't win
     against it - even when yours comes later in the file. */
  section table { font-size: 0.82em; margin: 0 auto; border-collapse: collapse; border: none; }
  section table th {
    border: none;
    border-top: 2px solid var(--ink);
    border-bottom: 1px solid var(--ink);
    font-family: 'Kreon', serif;
    font-weight: 600;
    padding: 0.4em 0.9em;
    background: none;
    color: var(--ink);
  }
  section table td { border: none; padding: 0.35em 0.9em; }
  section table tr:last-child td { border-bottom: 2px solid var(--ink); }
  section table tr { background: none; border-top: none; }

  /* ---------- 8. CODE ---------- */
  section pre, section code {
    font-family: 'IBM Plex Mono', monospace;
  }
  section pre {
    background: #ffffff;
    border-left: 3px solid var(--ink);
    border-radius: 0;
    padding: 0.8em 1em;
  }
  section code { background: rgba(21,42,74,0.06); border-radius: 0; padding: 0.05em 0.3em; }
  section pre code { background: none; padding: 0; }

  /* ---------- 9. IMAGE FILLING THE WHOLE SLIDE ----------
     The spine is hidden here on purpose (an edge-to-edge photo with
     a bar cut out of one side looks like a mistake, not a choice).
     The caption sits in a solid navy strip at the bottom instead of
     a dark fade laid over the photo. */
  section.imgcaption { padding: 0; background: none; }
  section.imgcaption h1 {
    position: absolute;
    left: 0; right: 0; bottom: 0;
    display: block;
    width: auto;
    background: var(--ink);
    color: #ffffff;
    border: none;
    margin: 0;
    padding: 0.5em 64px;
    font-size: 1.3em;
  }
---

<!--
_class: title
_paginate: false
-->

[//]: # (TITLE SLIDE. Replace the 4 logo files below with your own if your lab's logos change ; see the CSS note above the .logos rules for how to resize any one of them individually.)

# Your Presentation Title

### An optional subtitle ; delete this line if not needed

<p class="meta">Presented by: <span class="name">Your Full Name</span></p>
<p class="meta">Your Designation</p>
<p class="meta">21 September 2026</p>

<!-- Logos -->
<span class="logos">
  <!-- <img src="./media/dae_logo.svg" alt="DAE"> -->
  <img src="./media/hbni_logo.png" alt="HBNI">
  <img src="./media/NISER@20_logo.png" alt="NISER">
  <img src="./media/SMLAB_white.png" alt="SMLab">
</span>

[//]: # (The lines above use HTML tags so the name can be styled bigger than the designation/date, and so the logos can each have their own height/width. This needs --html ; see the note in the CSS section if these tags aren't showing up correctly.)

---



<!-- NOTE: Another example of title slide -->

<!-- _class: lead -->
<!-- _footer: '' -->
<!-- _paginate: false -->
<!-- _backgroundColor: #000 -->
<!-- _backgroundImage: url('./media/slide_bg_light.png') -->
![bg w:60% opacity:20%](./media/bg2.png)  

# **TITLE SLIDE VARIATION 2**

<p class="presenter-name">
  John Smith
</p>
<p class="lab-name">
  Subhankar Mishra Lab<br>
  Sep XX, 20XX
</p>

<div class="callout"><b>Note:</b>Add logos after this</div>


---


# Outline

[//]: # (Type the same names as your section slides. Numbered list = numbers appear automatically.)

1. Text and Lists
2. Boxes, Tables and Math
3. Code and Figures
4. Conclusion

---

# Bullet Points

- First level point
  - Second level point (indent with 2 spaces)
    - Third level point
- **Bold**, *italic*, `inline code`, ~~crossed out~~
- A [link to a website](https://marp.app)
- Images: `![w:400](file.png)` sets the width to 400 pixels

1. Numbered lists work too
2. Just start the line with a number

---

<!-- _class: cols -->

[//]: # (TWO COLUMNS. The class "cols" lays out two <div> boxes side by side with CSS Grid. Wrap each side's content in its own <div> — this needs --html, same as the title slide.)
 
# Two Columns
 
<div>

### Left side
 
- Point one
- Point two
- Point three
</div>
<div>

### Right side
 
- Point four
- Point five
- Point six
</div>


---

![bg right:38%](./media/img2.jpg)

[//]: # (IMAGE BESIDE TEXT. "bg right:38%" puts figure1.png on the right 38 percent of the slide. Use "bg left:38%" for the left side. Replace media/figure1.png with your file.)

# Text Next to an Image

- Keep text short
- One idea per slide
- The image fills the right side

---

# Split Slide 1

![bg right:45% w:90%](./media/img2.jpg)

* First point made here
* Second point made here
* Third point made here

---

# Split Slide 2

![bg right](./media/img2.jpg)

* First point made here
* Second point made here
* Third point made here


# A Note

> Any line starting with `>` becomes a note like this one. Use it for definitions or key ideas : the border is the only styling, no fill.

---

# Three Kinds of Callout

[//]: # (Needs --html: three colored callouts side by side aren't possible with plain blockquotes, since each one needs its own color. Without --html, use the plain "> Note:" style from the previous slide three times instead.)

<div class="callout"><b>Note</b>Use this for definitions or key ideas.</div>
<div class="callout warn"><b>Warning</b>Use this for important warnings or problems.</div>
<div class="callout good"><b>Good</b>Use this for examples that worked.</div>

---

# Table

| Method   | Accuracy (%) | Time (s) |
| :------- | :----------: | -------: |
| Baseline |     82.1     |     12.0 |
| **Ours** |   **89.4**   |      9.5 |

[//]: # (Column alignment: :--- left, :---: center, ---: right. Border style here matches the clean-line table style in the .tex deck: a line at the top and bottom, none in between.)

---

# Tables

<style scoped>
  table {
    /* NOTE: To make the table span the slide width */
    width: 100%;
    font-size: 24px;
  }
</style>

| Heading 1   | Heading 2   | Heading 3   |
|:------------|:-----------:|------------:|
|     abc     |    cde      |    fgh      |
|     123     |    456      |    789      |

---

# Math

Inline formula: $E = mc^2$

A formula on its own line:

$$
f(x) = \frac{1}{\sqrt{2\pi\sigma^2}}\, e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

---

# Equations

* Adjacency matrix:
  $$
  A_{ij} = \begin{cases}
    1, \quad & \text{if } i \text{ and } j \text{ are connected} \\
    0, \quad & \text{otherwise}
  \end{cases}
  $$
* Adjacency matrix for a SRG satisfies:
  $$
  \begin{align*}
  A^2 &= (k - \mu)I + \mu J + (\lambda - \mu)A \\
  JA &= AJ = kA \\
  J^2 &= NJ
  \end{align*}
  $$
* A graph with $N$ vertices has an $N\times N$ adjacency matrix. This problem is in the $NP$ complexity class and is purported to be NP-Intermediate (if $P \ne NP$).

---

# Code

```python
# A simple Python example
def greet(name):
    return "Hello, " + name

print(greet("World"))
```

[//]: # (Change "python" after the three backticks to c, cpp, java, javascript, bash, etc.)

---

* Here's some code:

  ```py
  def hello_world():
      print("Hello, World!")
  ```

* Here's some inline code: `print("Hello, World!")`
* Here's some code in a different language:

  ```julia
  function hello_world()
    println("Hello, World!")
  end
  ```

---

# Figure

![w:520](./media/img1.jpg)

*A short caption goes here, in italics, below the figure.*

[//]: # (Replace media/figure1.png with your file. If the file is missing, most places that show Markdown display the alt text instead ; Marp shows a broken-image icon with no text, so double-check the path before presenting.)

---

# Image Slide 1

<style scoped>
  img {
    border-radius: 50px;
  }
</style>

<!-- NOTE: Setting a background image of a particular width and height -->
![w:1100 h:250 opacity:1.0](./media/img1.jpg)

---

<!-- NOTE: Another example of image as a background -->
<!-- _paginate: false -->
<!-- _footer: '' -->
<style scoped>
  h1 {
    color: black;
  }
</style>

# Image Slide 2

![bg ](./media/img2.jpg)

---

<!-- NOTE: Another example of image as a background -->
<!-- _paginate: false -->
<!-- _footer: '' -->
<style scoped>
  h1 {
    color: black;
  }
</style>

# Image Slide 3

![bg](./media/img2.jpg)
![bg](./media/img2.jpg)

---

<!-- NOTE: Another example of image as a background -->
# Image Slide 4

![bg w:100%](./media/img2.jpg)
![bg w:100%](./media/img2.jpg)

---


<!-- _class: imgcaption -->

![bg](./media/img2.jpg)

# A figure that fills the whole slide

[//]: # (IMAGE FILLING THE WHOLE SLIDE. "![bg]" with nothing after "bg" fills the whole slide. The heading becomes a solid navy caption strip pinned to the bottom instead of text floating over the photo.)

---

# Summary

- **Main message:** say it in one sentence
- **Key result:** one number or one picture
- **Next steps:** what happens after this talk

<!--
This is a SPEAKER NOTE. Only you see it (in presenter view).
Marp turns any normal HTML comment into a note like this one.
-->

---

# References

1. D. Knuth, *The TeXbook*, Addison-Wesley, 1984.
2. L. Lamport, *LaTeX: A Document Preparation System*, 2nd ed., 1994.

[//]: # (Marp has no automatic bibliography like the .bib setup in the .tex deck — list references by hand here.)

---

# References 2

* [Link to GitHub repo for the code](https://github.com/JeS24/CTQW-graph-isomorphism)
* Main papers:
  1. Rudinger et al; [Noninteracting multiparticle quantum random walks applied to the graph isomorphism problem for strongly regular graphs](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.86.022334)
  2. Gamble et al; [Two-particle quantum walks applied to the graph isomorphism problem](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.81.052313)

* Image sources:
  * [Title Slide Variations 1 & 2](#title-slide-variation-1)
    * [pxfuel](https://www.pxfuel.com/en/desktop-wallpaper-iqgfc)
    * [HiClipart](https://www.hiclipart.com/free-transparent-background-png-clipart-pgsow)
  * [Image Slide 1](#image-slide-1) - [ShutterStock](https://www.shutterstock.com/image-vector/set-funny-eggs-on-brown-background-2118472637)



---

<!--
_class: title
_paginate: false
-->

# Thank You

### Questions?

<p class="meta">your.email@example.com · www.yourwebsite.com</p>

---

[//]: # (Slides after this point are extra material. Only show them if someone asks. They still count in "page x / y".)

# Backup Slide

Extra details that you only show if someone asks.