---
name: TableCaptains Form System
description: >
  A utilitarian, high-contrast registration/RSVP form language. Flat white
  cards sit on a pale lavender page. Fields wear crisp black hairlines on
  a faintly tinted ghost-white fill. The only saturated color is a single
  confident blue — reserved for controls the user must act on: checkboxes,
  radios, and the continue button. Nothing floats, nothing glows, nothing
  gradients. Typography is set in Arial, slightly oversized, so the form
  reads like a printed questionnaire rather than a chromed web app.

colors:
  page:
    background: "#f5f6fc"        # soft lavender-gray, the outermost surface
    canvas:     "#e6e6e6"        # neutral gray for the max-width frame behind the card
  surface:
    card:       "#ffffff"        # the form card and footer bar
    field:      "#f8f8ff"        # "ghost white" — fill for inputs, selects, checkboxes, radio chips, and legal boxes
    overlay:    "rgba(255, 255, 255, 0)"  # invisible hit target wrapping small controls
  text:
    primary:    "#000000"        # titles, labels, values, button copy on light surfaces
    on-accent:  "#ffffff"        # copy on the primary blue button
    placeholder:"rgba(0, 0, 0, 0.5)"   # input placeholder and un-selected dropdown value
    icon-muted: "rgba(0, 0, 0, 0.65)"  # caret and clear glyphs inside selects
  border:
    field:      "#000000"        # 1px inset rule around text inputs and the amount field
    box:        "#000000"        # 1px solid rule around the legal-copy box
    selector:   "#3881f1"        # checkbox square and radio ring
  accent:
    primary:         "#3881f1"   # continue button fill, checkbox stroke, radio stroke
    primary-border:  "#3881f1"   # doubled 2px ring on the primary button
  focus:
    ring: "#3881f1"              # adopt the accent for :focus-visible (not present in source, inferred for accessibility)

typography:
  font-families:
    sans:     "Arial, 'Helvetica Neue', Helvetica, sans-serif"
    numeric:  "Inter, 'Helvetica Neue', Arial, sans-serif"   # used only for the '$' prefix in the amount field
    icon:     "'Font Awesome 6 Pro', sans-serif"             # caret ⌄ and clear ×
  scale:
    question-title:
      font-family: sans
      font-weight: 400
      font-size: "32px"
      line-height: "normal"    # ~1.15
      letter-spacing: "0"
      text-align: center
      color: text.primary
    field-label:
      font-family: sans
      font-weight: 700
      font-size: "14px"
      line-height: "20px"
      letter-spacing: "0.5px"
      text-transform: none
      color: text.primary
    checkbox-label:
      font-family: sans
      font-weight: 700
      font-size: "14px"
      line-height: "20px"
      letter-spacing: "0.35px"
    input-value:
      font-family: sans
      font-weight: 400
      font-size: "20px"
      line-height: "normal"    # ~1.15
      letter-spacing: "1px"
      color: text.primary
    placeholder:
      font-family: sans
      font-weight: 400
      font-size: "20px"
      line-height: "normal"
      letter-spacing: "1px"
      color: text.placeholder
    option-label:
      font-family: sans
      font-weight: 400
      font-size: "20px"
      line-height: "30px"      # radio option rows use 30px lh
      letter-spacing: "0"
    legal-body:
      font-family: sans
      font-weight: 400
      font-size: "20px"
      line-height: "normal"
    currency-prefix:
      font-family: numeric
      font-weight: 700
      font-size: "16px"
      line-height: "24px"
      letter-spacing: "-0.3125px"
    button-label:
      font-family: sans
      font-weight: 400
      font-size: "20px"
      line-height: "normal"
      letter-spacing: "0"
      color: text.on-accent
      text-align: center

spacing:
  base-unit: "4px"
  scale:
    "0":   "0"
    "1":   "4px"      # tightest (between label and input)
    "2":   "8px"      # small icon gaps, button inner padding
    "3":   "12px"     # field inner padding top/bottom, radio chip inner padding
    "4":   "16px"     # standard gap between sections inside a card; field horizontal padding
    "6":   "24px"     # control size (checkbox / radio diameter)
    "10":  "40px"     # card padding (all sides of card content)
  form:
    card-padding-x:       "40px"
    card-padding-top:     "40px"
    card-padding-bottom:  "40px"
    section-gap:          "16px"    # title -> controls
    field-label-gap:      "4px"
    field-row-gap:        "4px"     # between stacked field rows within a block
    two-col-gutter:       "4px"     # 306px - 302px between half-width fields
    option-chip-v-gap:    "16px"    # vertical gap between stacked radio/checkbox chips
    option-chip-h-gap:    "12px"    # 310 - 298 between side-by-side chips
    input-padding-x:      "16px"
    input-padding-y:      "12px"
    chip-padding:         "13px"    # uniform inset for radio/checkbox option chips
    footer-padding-y:     "16px"
    footer-padding-x:     "260.5px" # wide side gutters keep the CTA anchored right on 1665px canvas

sizing:
  form-card-width:     "688px"
  form-column-width:   "302px"    # half-width fields (city/state, zip/country)
  option-chip-width:   "296px"    # a single checkbox/radio option chip (half of form body)
  option-chip-wide:    "298px"    # the donation radio chips (slightly different)
  option-chip-height:  "50px"     # checkbox chip
  radio-chip-height:   "56px"     # donation radio chip (taller to seat the 24px ring)
  input-height:        "47px"
  control-size:        "24px"     # checkbox square / radio circle
  button-height:       "51px"
  button-min-width:    "132px"
  footer-bar-height:   "83px"

radii:
  none:    "0"
  xs:      "4px"      # checkbox box, legal-copy container
  sm:      "8px"      # all text inputs, selects, radio chips, amount field
  lg:      "16px"     # outer card corners (top of first section, bottom of last)
  full:    "9999px"   # primary button (pill)
  circle:  "50%"      # radio ring

borders:
  hairline-field:
    style: inset
    spec: "inset 0 0 0 1px #000000"     # text inputs: black hairline rendered as inset shadow (no layout shift)
  hairline-box:
    style: solid
    spec: "1px solid #000000"           # legal-copy box, amount field outer wrapper
  selector-ring:
    style: solid
    spec: "1px solid #3881f1"           # checkbox square outline
  radio-ring:
    style: solid
    spec: "2px solid #3881f1"           # radio circle stroke (heavier than checkbox)
  button-ring:
    style: solid
    spec: "2px solid #3881f1"           # doubled ring around primary button (same color as fill)
  select-rest:
    style: none
    spec: "inset 0 0 0 0 #000000"       # selects render borderless at rest; only the fill differentiates them

shadows:
  none: "none"
  # The system uses no drop shadows. Depth is communicated by surface color
  # (page → canvas → card → field), not by elevation.

elevation:
  card:    "0"       # flat white, no shadow
  field:   "0"       # flat tinted fill, no shadow
  button:  "0"       # flat blue pill, no shadow
  footer:  "0"       # sticky-looking but unshaded

motion:
  # Not specified in the source. Defaults below are inferred for
  # interactive parity; tune to taste.
  duration:
    instant: "0ms"
    fast:    "120ms"
    base:    "180ms"
  easing:
    standard: "cubic-bezier(0.2, 0, 0, 1)"
    emphasized: "cubic-bezier(0.2, 0, 0, 1.2)"
  transitions:
    field-focus:  "box-shadow 120ms cubic-bezier(0.2, 0, 0, 1)"
    checkbox-tick:"background-color 120ms linear, border-color 120ms linear"
    button-press: "transform 120ms cubic-bezier(0.2, 0, 0, 1), background-color 120ms linear"

breakpoints:
  # Inferred. Source canvas renders at 1665px desktop; card locks to 688px.
  sm: "480px"
  md: "768px"
  lg: "1024px"
  xl: "1280px"
  xxl: "1536px"

layout:
  page:
    background: page.background
    min-height: "100vh"
  canvas:
    background: page.canvas
    max-width: "1665px"
    padding-top: "40px"
  form-card:
    background: surface.card
    width: "688px"
    corner-radius-top: "16px"
    corner-radius-bottom: "16px"
    subsection-stacking: "flush"   # sections are flush-stacked inside one card; only the first gets a top radius, only the last gets a bottom radius
  footer-bar:
    background: surface.card
    height: "83px"
    alignment: "cta-right"
    position: "below card, full-bleed"

components:
  question-title:
    description: "Centered 32px Arial at the top of every section."
    tokens:
      typography: typography.scale.question-title
      padding-bottom: spacing.form.section-gap
      required-marker: "trailing * in same weight/size"

  text-input:
    description: "The default field. Ghost-white fill, 1px inset black hairline, 8px radius."
    tokens:
      height: sizing.input-height
      padding: "12px 16px"
      radius: radii.sm
      background: surface.field
      border: borders.hairline-field
      placeholder: typography.scale.placeholder
      value: typography.scale.input-value

  select:
    description: "Same silhouette as text-input but renders borderless at rest. Caret (FA ⌄) sits at the right edge. The country picker additionally shows a flag glyph and a clear (×) affordance."
    tokens:
      height: sizing.input-height
      padding: "12px 16px"
      radius: radii.sm
      background: surface.field
      border: borders.select-rest
      caret-color: text.icon-muted
      clear-color: text.icon-muted

  checkbox:
    description: "24px blue-stroked square with a ghost-white fill. Label sits to the right in bold 14px."
    tokens:
      size: sizing.control-size
      radius: radii.xs
      background: surface.field
      border: borders.selector-ring
      label: typography.scale.checkbox-label

  radio:
    description: "24px blue ring, 2px stroke, transparent fill. Often presented inside a chip."
    tokens:
      size: sizing.control-size
      radius: radii.circle
      border: borders.radio-ring
      background: "transparent"

  option-chip:
    description: "A tappable row that wraps a checkbox or radio plus a value. Ghost-white fill, 1px black hairline, 8px radius, 13px inner padding. Used for 'What is your favorite color?' (checkbox variant) and 'Please consider a donation' (radio variant)."
    tokens:
      padding: spacing.form.chip-padding
      radius: radii.sm
      background: surface.field
      border: borders.hairline-box
      v-gap: spacing.form.option-chip-v-gap
      h-gap: spacing.form.option-chip-h-gap

  legal-box:
    description: "A scroll-ready container for terms text. Black 1px hairline, 4px radius, ghost-white fill, 25px top padding so copy doesn't kiss the border."
    tokens:
      radius: radii.xs
      background: surface.field
      border: borders.hairline-box
      padding-top: "25px"
      padding-x: "17px"
      body: typography.scale.legal-body

  amount-field:
    description: "A text input with a leading '$' badge. The badge shares the field fill but is visually seamed by the outer black hairline at 8px radius."
    tokens:
      height: sizing.input-height
      radius: radii.sm
      background: surface.field
      border: borders.hairline-box
      prefix-width: "42px"
      prefix-typography: typography.scale.currency-prefix

  primary-button:
    description: "Pill-shaped CTA. Solid blue fill, doubled 2px blue ring, white Arial 20px label."
    tokens:
      height: sizing.button-height
      min-width: sizing.button-min-width
      radius: radii.full
      background: accent.primary
      border: borders.button-ring
      label: typography.scale.button-label
      padding-x: "24px"

  footer-bar:
    description: "Full-bleed white bar directly under the form card; the Continue button floats to the right edge of the card column."
    tokens:
      height: sizing.footer-bar-height
      background: surface.card
      padding-y: spacing.form.footer-padding-y
      cta-alignment: right

states:
  # Not depicted in the source — listed so implementation stays consistent with the resting style.
  field:
    rest:
      background: surface.field
      border: borders.hairline-field
    hover:
      border: "inset 0 0 0 1px #000000"   # unchanged; hover is for cursor only
    focus:
      border: "inset 0 0 0 2px #3881f1"   # promote to blue 2px inset on focus
    error:
      border: "inset 0 0 0 2px #c0392b"   # suggested: a muted red at similar weight
  button-primary:
    rest:
      background: accent.primary
      border: borders.button-ring
    hover:
      background: "#2f6dd0"
    pressed:
      background: "#255aba"
    disabled:
      background: "rgba(56, 129, 241, 0.4)"
      color: text.on-accent

accessibility:
  min-tap-target: "24px control, chip expands it to 50px+"
  placeholder-is-not-label: true     # every field has a bold label; placeholder is exemplar text only
  required-indicator: "asterisk suffix in the question title (e.g. 'Zipcode*')"
  color-only-signals: none           # the accent is always paired with a shape (ring, tick, fill)

---

# TableCaptains Form System

## Overall feel

The form reads like a clean government or civic questionnaire: printed,
serif-adjacent in spirit (even though the typeface is Arial), and
unapologetically rectangular. Sections aren't cards — they're **slices
of a single card**. They stack flush against one another with no gap and
no dividers. Only the first slice gets a rounded top; only the last gets
a rounded bottom. The result is one tall object that feels bound at the
edges.

The page around it is never loud. A pale lavender-gray (`#f5f6fc`)
washes the whole viewport, framed at the center by a slightly deeper
neutral canvas (`#e6e6e6`) that hints at a max-width gutter. The white
card is the brightest surface on the page, and that's the point —
**content comes forward by being lighter, not by being shadowed**.

## Color discipline

There are only five colors doing real work:

1. **Page lavender** (`#f5f6fc`) — the quietest layer.
2. **Canvas gray** (`#e6e6e6`) — the frame behind the card.
3. **Card white** (`#ffffff`) — the form itself.
4. **Ghost white** (`#f8f8ff`) — the fill for every input, select,
   chip, and legal-copy box. It's white with a barely perceptible
   lavender tint so fields don't disappear against the card.
5. **Signal blue** (`#3881f1`) — used only on controls that *take an
   action or hold a decision*: checkbox strokes, radio rings, and the
   Continue button. If something isn't blue, you can't commit with it.

Black is structural, not decorative: it draws the 1px hairlines around
fields and boxes. Everything else is grayscale transparency
(`rgba(0,0,0,0.5)` for placeholder text, `rgba(0,0,0,0.65)` for muted
icons like the select caret).

## Typography

Arial does almost all the talking. The scale is deliberately short:

- **32px regular** for every question ("What is your mailing address?")
- **20px regular** for input values, placeholders, option labels, and
  the button
- **14px bold** with +0.5px tracking for small field labels (Street,
  City, Zipcode…)

The 32/20/14 triad is wide enough to create a clear hierarchy with
only one family. The only exception is the `$` prefix in the amount
field, which is set in a tighter numeric sans at 16px Bold — a small
nod that money fields feel numeric.

Question titles are **center-aligned**. Field labels are
**left-aligned** and sit tight above their inputs (4px gap). This
keeps questions feeling formal and field labels feeling operational.

## Fields and controls

Text inputs are the workhorse. The recipe never changes:

- 8px corner radius
- Ghost-white fill
- 1px black hairline, rendered as an **inset shadow** so focus can
  promote the line weight without shifting layout
- 47px tall, 12×16px padding

Selects are the same silhouette — but they render with **no visible
border** at rest. The ghost-white fill alone is enough to read them as
a field, and a muted caret (`⌄`) at the right edge confirms it. The
country picker additionally uses an emoji flag and an `×` clear
glyph; both are muted to keep the accent blue reserved for action.

Checkboxes and radios are the only places color leaks into the field
layer. Checkboxes are 24px blue-stroked squares with a 4px radius.
Radios are 24px blue rings with a heavier 2px stroke. Both are
presented either naked (next to a small label) or wrapped in an
**option chip** — a ghost-white rounded rectangle with a 1px black
hairline that makes the entire row tappable.

Option chips are laid out in a 2-column grid at half the card width
(296–298px), stacking vertically inside their section. This gives the
form a rhythmic grid feel without committing to a heavy table.

## Buttons

There is one button. It's a **pill** — fully rounded, fully
saturated signal blue, with a doubled 2px blue ring that makes the
edge read as intentionally weighty rather than accidental. White
20px Arial label. No gradient, no shadow, no hover glow specified.
The button lives in a **separate white bar directly below the form
card**, floated to the right edge. The bar is full-bleed, so the
button reads as a commitment rail rather than something inside the
form.

## Spatial rhythm

The card is **688px wide** and never flexes wider. Inside it, the
padding is uniform: 40px on all sides of the content area. Sections
within the card use a 16px gap between the question title and its
controls. Fields stack at 4px between label and input, and rows of
fields stack with a small inter-row gap that lets the black hairlines
breathe without adding visual clutter.

Two-column fields (City/State, Zip/Country) use a **4px gutter** —
unusually tight. This is intentional: the hairlines are so fine that a
wider gutter would make paired fields feel disconnected. At 4px, the
eye reads them as a single row with a seam.

Radio and checkbox chips use a wider **12px horizontal** and **16px
vertical** gutter, because their outer hairline is a full rule
rather than an inset shadow and needs breathing room.

## Surface stack

Depth is communicated entirely through surface color, never through
shadow:

```
page (#f5f6fc)
  └── canvas (#e6e6e6)
        └── card (#ffffff)
              └── field / chip / legal box (#f8f8ff)
```

Each level darkens or lightens by roughly one perceptual step. Because
the steps are small, the whole UI feels **one plane thick**, which
suits a form: there is nothing to dismiss, nothing floating, and no
hierarchy to get lost in.

## Iconography

Icons come from Font Awesome 6 Pro and are used sparingly:
- `⌄` (chevron down) for select carets
- `×` (close) for the country-picker clear
- Emoji flag for country identity

All icons render at 25px with a muted `rgba(0,0,0,0.65)` color so
they don't compete with the blue accents.

## Motion

Not specified in the source. A reasonable default is fast (120ms),
standard-eased transitions on focus rings and checkbox ticks. Avoid
lifts, scale bounces, or anything that contradicts the flat, printed
feel. A button press should darken the fill, not shadow it.

## Writing and voice

The form copy is plain and direct — *"What is your mailing address?"*,
*"Please review the terms"*, *"Please consider a donation."* —
sentence-cased, question-marked, asterisked when required. Labels are
single words (Street, City, Zipcode) and placeholders are literal
examples (Address Line 1, Zip Code). Keep this tone: **ask politely,
label tersely, placeholder descriptively.**

## What this system is *not*

- It is **not** a glassmorphism or neumorphism system. No blurs, no
  inner glows, no gradients.
- It is **not** a Material-style elevation system. Cards do not float;
  buttons do not cast.
- It is **not** a brand-expressive design language. Color is used
  semantically (accent = action) rather than decoratively.

If a future component tempts you toward a shadow, a gradient, or a
second saturated color, resist it. The entire identity of this form
system lives in the tension between **stark black hairlines** and
**one confident blue**.
