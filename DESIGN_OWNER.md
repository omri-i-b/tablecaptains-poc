---
name: TableCaptains Owner Console
description: >
  A purple-forward SaaS dashboard for the person running the event. Where
  the guest form is stark black-on-white, the owner console is warm,
  shadowed, and dense. A deep brand purple anchors navigation and primary
  actions; a supporting blue handles read-only affordances like preview
  and invite. Cards live on a pale lilac canvas with a soft 1px shadow,
  and modals dim the world with a translucent purple veil. Typography is
  set in Inter across a compressed scale (12 / 14 / 16 / 18), giving the
  UI the clipped, operator-tool feel of an admin surface rather than a
  consumer form.

colors:
  brand:
    primary:         "#372056"   # deep brand purple — primary buttons, active nav text, "My Events"
    primary-hover:   "#45286b"   # slightly lifted purple for hover/active-press states
    primary-ink:     "#191236"   # near-black violet — headings, body copy on light surfaces
    primary-soft:    "#ebecf6"   # the lilac tint used for selected nav highlight and hairline borders
    primary-veil:    "rgba(25, 18, 54, 0.5)"   # modal backdrop — brand purple at 50%
  accent:
    blue:            "#3d91ff"   # secondary action color — "Preview", "Invite Team Members"
    blue-soft:       "#eff6ff"   # pale blue notification / info surface
  surface:
    page:            "#f5f6fc"   # outer page (sidebar background)
    canvas:          "#e8e8ed"   # main content canvas behind cards
    card:            "#ffffff"   # all cards, modals, fields
    divider:         "#e1e1e1"   # horizontal section dividers inside modals / cards
    border-soft:     "#d8d8e3"   # card hairlines and dropdown borders
    field-hairline:  "#ebecf6"   # 1px inset on form inputs (very subtle)
  text:
    primary:         "#191236"   # headings
    body:            "#372056"   # body copy and form labels
    muted:           "#5e5972"   # subtitles, field helper text, inactive nav
    faint:           "#a5a5ac"   # placeholders, disabled labels
    on-brand:        "#ffffff"   # white text on purple buttons
    on-blue:         "#ffffff"   # white text on blue buttons
    link:            "#3d91ff"   # inline text links
  status:
    success:         "#09a96f"   # "Published" badge foreground
    success-soft:    "#d9f2e9"   # "Published" badge background
    warning:         "#f59e0b"   # "Services with minor issues" label and dot
    danger:          "#e3414b"   # error states, unread/alert dot on avatar
  shadow:
    ink-5:           "rgba(0, 0, 0, 0.05)"
    ink-10:          "rgba(0, 0, 0, 0.1)"

typography:
  font-families:
    sans:  "Inter, 'Helvetica Neue', Arial, sans-serif"
    icon:  "'Font Awesome 6 Pro', sans-serif"
  weights:
    regular:   400
    semibold:  600
    black:     900    # reserved for heavy solid icon glyphs
  scale:
    page-title:
      font-family: sans
      weight: semibold
      font-size: "20px"
      line-height: "28px"
      letter-spacing: "-0.1px"
      color: text.primary
    modal-title:
      font-family: sans
      weight: semibold
      font-size: "18px"
      line-height: "26px"
      color: text.primary
    modal-subtitle:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.muted
    section-header:
      font-family: sans
      weight: semibold
      font-size: "16px"
      line-height: "24px"
      color: text.primary
    body:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.body
    label:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.body
    input-value:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.primary
    placeholder:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.faint
    button-label:
      font-family: sans
      weight: semibold
      font-size: "14px"
      line-height: "20px"
      letter-spacing: "0"
    helper-tip:
      font-family: sans
      weight: regular
      font-size: "12px"
      line-height: "18px"
      color: text.muted
    caption:
      font-family: sans
      weight: regular
      font-size: "12px"
      line-height: "16px"
      color: text.muted
    nav-item:
      font-family: sans
      weight: regular
      font-size: "14px"
      line-height: "20px"
      color: text.muted
    nav-item-active:
      font-family: sans
      weight: semibold
      font-size: "14px"
      line-height: "20px"
      color: brand.primary
    badge:
      font-family: sans
      weight: semibold
      font-size: "12px"
      line-height: "16px"
      letter-spacing: "0.2px"

spacing:
  base-unit: "4px"
  scale:
    "0":   "0"
    "1":   "4px"
    "2":   "8px"
    "3":   "12px"
    "4":   "16px"
    "5":   "20px"
    "6":   "24px"
    "8":   "32px"
    "10":  "40px"
  layout:
    sidebar-width:        "200px"
    sidebar-item-pad-x:   "12px"
    sidebar-item-pad-y:   "8px"
    topbar-height:        "56px"
    topbar-pad-x:         "24px"
    canvas-pad:           "24px"
  card:
    pad-x:                "24px"
    pad-y:                "24px"
  modal:
    pad-x:                "24px"
    pad-top:              "20px"
    pad-bottom:           "16px"
    header-gap:           "4px"     # title -> subtitle
    body-gap:             "20px"    # between field groups
    footer-gap:           "12px"    # between footer buttons
  field:
    label-gap:            "6px"
    row-gap:              "16px"
    col-gap:              "24px"
    input-pad-x:          "12px"
    input-pad-y:          "8px"

sizing:
  sidebar-width:         "200px"
  topbar-height:         "56px"
  input-height:          "36px"
  button-height-sm:      "32px"
  button-height-md:      "36px"
  button-height-lg:      "40px"
  avatar-sm:             "24px"
  avatar-md:             "32px"
  avatar-lg:             "40px"
  toggle-width:          "36px"
  toggle-height:         "20px"
  toggle-thumb:          "16px"
  modal-width:           "624px"
  modal-max-width:       "90vw"
  promo-card-width:      "176px"

radii:
  none:       "0"
  xs:         "3px"       # toggle thumb
  sm:         "4px"       # badges, small chips
  md:         "6px"       # nav item highlight, inputs, secondary buttons
  lg:         "8px"       # cards, modals, primary buttons, form controls
  xl:         "16px"      # promo / illustration card
  pill:       "100px"     # status badges, rounded CTAs
  full:       "9999px"    # avatars, dots, circular icon chips

borders:
  card:
    spec: "1px solid #d8d8e3"
  divider:
    spec: "1px solid #e1e1e1"
  field-rest:
    spec: "inset 0 0 0 1px #ebecf6"      # extremely subtle — inputs whisper their edge
  field-focus:
    spec: "inset 0 0 0 2px #3d91ff"      # promote to blue ring on focus
  nav-active:
    spec: "none"                          # active nav is indicated by fill, not stroke

shadows:
  none:   "none"
  hair:   "0 0 0 0 #ffffff"                                          # null-shadow placeholder
  xs:     "0 1px 2px 0 rgba(0, 0, 0, 0.05)"                          # card surface lift
  sm:     "0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.1)"  # buttons / inputs
  lg:     "0 10px 15px 0 rgba(0, 0, 0, 0.1), 0 4px 6px 0 rgba(0, 0, 0, 0.1)" # modals and overlays

elevation:
  level-0:
    usage: "page / canvas"
    shadow: none
  level-1:
    usage: "cards, sidebar surfaces, inline panels"
    shadow: shadows.xs
  level-2:
    usage: "buttons, inputs at rest, sticky bars"
    shadow: shadows.sm
  level-3:
    usage: "modals, popovers, toasts"
    shadow: shadows.lg

motion:
  duration:
    instant: "0ms"
    fast:    "120ms"
    base:    "180ms"
    slow:    "240ms"
  easing:
    standard: "cubic-bezier(0.2, 0, 0, 1)"
    enter:    "cubic-bezier(0.2, 0.8, 0.2, 1)"
    exit:     "cubic-bezier(0.4, 0, 1, 1)"
  transitions:
    field-focus:   "box-shadow 120ms cubic-bezier(0.2, 0, 0, 1)"
    toggle-thumb:  "transform 180ms cubic-bezier(0.2, 0, 0, 1), background-color 180ms linear"
    modal-enter:   "opacity 180ms cubic-bezier(0.2, 0.8, 0.2, 1), transform 180ms cubic-bezier(0.2, 0.8, 0.2, 1)"
    modal-exit:    "opacity 120ms cubic-bezier(0.4, 0, 1, 1)"
    backdrop:      "opacity 180ms linear"
    hover-bg:      "background-color 120ms linear"

breakpoints:
  sm: "640px"
  md: "768px"
  lg: "1024px"
  xl: "1280px"
  xxl: "1440px"
  design-canvas: "1680px"    # the source Figma frame

layout:
  app-shell:
    frame: "sidebar (200px) + main column (fluid)"
    background: surface.page
    sidebar-background: surface.page
    canvas-background: surface.canvas
    topbar-background: surface.card
    topbar-height: sizing.topbar-height
    topbar-border-bottom: borders.card

components:
  sidebar:
    background: surface.page
    width: sizing.sidebar-width
    padding: "16px 12px"
    section-gap: "24px"
    item:
      padding: "8px 12px"
      radius: radii.md
      typography: typography.scale.nav-item
      hover-background: brand.primary-soft
    item-active:
      background: brand.primary-soft
      typography: typography.scale.nav-item-active
    divider:
      margin-y: "16px"
      style: "1px solid"
      color: surface.border-soft
    promo-card:
      width: sizing.promo-card-width
      background: surface.card
      radius: radii.xl
      shadow: shadows.xs
      padding: "16px"
      image-treatment: "full-bleed illustration at top"
      cta: accent.blue

  topbar:
    height: sizing.topbar-height
    padding-x: spacing.layout.topbar-pad-x
    background: surface.card
    border-bottom: borders.card
    elements:
      - event-title (center, typography.scale.page-title, weight: regular)
      - published-badge (status.success-soft / status.success)
      - preview-link (accent.blue, inline)
      - services-warning (status.warning + red dot)
      - user-avatar (40px, radii.full)

  card:
    background: surface.card
    border: borders.card
    radius: radii.lg
    shadow: shadows.xs
    padding: spacing.card

  modal:
    backdrop: brand.primary-veil
    background: surface.card
    radius: radii.lg
    shadow: shadows.lg
    width: sizing.modal-width
    max-width: sizing.modal-max-width
    header:
      padding: "20px 24px 16px"
      title: typography.scale.modal-title
      subtitle: typography.scale.modal-subtitle
      divider-below: borders.divider
    body:
      padding: "20px 24px"
      gap: spacing.modal.body-gap
    footer:
      padding: "16px 24px"
      divider-above: borders.divider
      layout: "cancel left · secondary + primary right"
      gap: spacing.modal.footer-gap

  text-input:
    height: sizing.input-height
    padding: "8px 12px"
    radius: radii.md
    background: surface.card
    border: borders.field-rest
    placeholder: typography.scale.placeholder
    value: typography.scale.input-value

  time-input:
    description: "Borderless variant used for time pairs inside modals. The underline implied by the field hairline is enough — no boxed frame."
    height: sizing.input-height
    padding: "8px 0"
    background: "transparent"
    border: "none"
    border-bottom: "1px solid #ebecf6"
    placeholder: typography.scale.placeholder
    value: typography.scale.input-value

  toggle:
    width: sizing.toggle-width
    height: sizing.toggle-height
    radius: radii.pill
    track-off: "#d8d8e3"
    track-on: brand.primary
    thumb-size: sizing.toggle-thumb
    thumb-color: surface.card
    thumb-shadow: shadows.sm
    label-gap: "8px"

  button-primary:
    background: brand.primary
    hover-background: brand.primary-hover
    color: text.on-brand
    border: none
    radius: radii.lg
    height: sizing.button-height-md
    padding-x: "16px"
    shadow: shadows.sm
    typography: typography.scale.button-label
    disabled:
      background: "#b5a9c4"
      color: text.on-brand

  button-secondary-text:
    description: "Ghost/link button used for 'Cancel' and '+ Save & add another'. No fill, no border."
    background: transparent
    color: text.body
    typography: typography.scale.button-label
    hover-color: brand.primary
    padding: "8px 12px"

  button-blue:
    description: "Used for read-only or onboarding actions: Preview link, Invite Team Members."
    background: accent.blue
    color: text.on-blue
    radius: radii.md
    height: sizing.button-height-sm
    padding-x: "12px"
    shadow: shadows.sm
    typography: typography.scale.button-label

  badge-status:
    radius: radii.pill
    padding: "2px 10px"
    typography: typography.scale.badge
    variants:
      published:
        background: status.success-soft
        color: status.success
      warning:
        background: "transparent"
        color: status.warning
        icon: status.warning

  page-header:
    description: "The '<icon> Agenda' / 'Create and manage agenda items…' pair at the top of a content area."
    icon-size: "24px"
    icon-color: text.muted
    title: typography.scale.section-header
    subtitle: typography.scale.body
    gap: "4px"

  cta-button-large:
    description: "Centered action like 'Build your Agenda'."
    background: brand.primary
    color: text.on-brand
    radius: radii.lg
    height: sizing.button-height-lg
    padding-x: "20px"
    shadow: shadows.sm
    typography: typography.scale.button-label

  avatar:
    sizes: [avatar-sm, avatar-md, avatar-lg]
    radius: radii.full
    ring: "2px solid #ffffff"            # when sitting on the topbar
    status-dot:
      size: "8px"
      color: status.danger
      position: "top-right"

  help-bubble:
    description: "Floating circular widget in the bottom-right corner."
    size: "48px"
    radius: radii.full
    background: surface.card
    shadow: shadows.lg
    badge-count:
      background: status.danger
      color: text.on-brand
      size: "16px"

states:
  field:
    rest:     { border: borders.field-rest }
    hover:    { border: "inset 0 0 0 1px #d8d8e3" }
    focus:    { border: borders.field-focus }
    disabled: { background: "#f5f6fc", color: text.faint }
    error:    { border: "inset 0 0 0 2px #e3414b" }
  button-primary:
    rest:     { background: brand.primary }
    hover:    { background: brand.primary-hover }
    pressed:  { background: "#2c1a43" }
    disabled: { background: "#b5a9c4" }
  nav-item:
    rest:     { background: "transparent", color: text.muted }
    hover:    { background: brand.primary-soft, color: brand.primary }
    active:   { background: brand.primary-soft, color: brand.primary, weight: semibold }

accessibility:
  focus-visible: "2px inset ring in accent.blue on fields; 2px outline offset 2px on buttons"
  min-tap-target: "32px minimum; icon-only targets padded to 36px"
  required-indicator: "trailing '*' after the label, not color-only"
  contrast:
    body-text-on-card: "#191236 on #ffffff — AAA"
    muted-text-on-card: "#5e5972 on #ffffff — AA"
    primary-button: "#ffffff on #372056 — AAA"
    placeholder: "#a5a5ac on #ffffff — AA large only (do not use for meaningful copy)"

---

# TableCaptains Owner Console

## Overall feel

The owner console is a **purple-accented SaaS workspace** for the
person running an event. The guest form is terse and printed; this
surface is lived-in and dense. It has an app shell, a sidebar, a top
bar, shadows, status badges, and a help bubble tucked in the corner.
The color palette is warmer, the typography is tighter, and — unlike
the guest form — **cards actually float** on their canvas with a
hair-thin shadow.

Think of it as an airline ops console, not a public kiosk.

## Color system

A **deep brand purple** (`#372056`) carries the identity. It's used for:
- Primary buttons (Save, Build your Agenda)
- Active nav text
- The "My Events" link at the bottom of the sidebar
- As a 50%-opacity **veil** (`rgba(25,18,54,0.5)`) behind every modal

It's paired with a **lilac tint** (`#ebecf6`) that shows up as:
- The selected-nav background pill
- The inset hairline on form fields
- Any "quiet" treatment that still needs to feel family-owned

A **supporting blue** (`#3d91ff`) is the second actor. It's used for
actions that are *informational* rather than *decisional* — the "Preview"
link in the top bar, the "Invite Team Members" button in the promo card,
inline text links. When the system wants you to *commit*, it goes
purple; when it wants you to *explore*, it goes blue.

Status lives in its own register:
- **Green** (`#09a96f` on `#d9f2e9`) — Published badge
- **Amber** (`#f59e0b`) — "Services with minor issues"
- **Red** (`#e3414b`) — the 8px avatar dot and the help-bubble counter

Backgrounds step through cool grays: sidebar on the palest lavender
(`#f5f6fc`), the main canvas a touch darker (`#e8e8ed`), and cards pure
white with a `1px solid #d8d8e3` hairline plus a 1px 5%-black shadow.
The steps are small on purpose — the whole interface should feel like
**one cohesive workspace**, not a stack of floating panes.

## Typography

Inter, always. The scale is short and administrative:

- **20 Semi-Bold** — page titles
- **18 Semi-Bold** — modal titles
- **16 Semi-Bold** — section headers
- **14 Regular / Semi-Bold** — everything else (labels, inputs, buttons,
  nav items, body copy)
- **12 Regular** — tips, captions, badge text

There are no marketing-sized headlines here. The tallest thing on any
screen is usually the modal title at 18px. That density is the point:
an operator opens ten screens an hour and needs every one to hand them
information fast.

Weight does the hierarchy, not size. Active nav and button labels go
Semi-Bold; everything resting stays Regular.

## Elevation and shadow

Unlike the guest form (which uses none), this system uses **three
shadow levels**, each tiny and restrained:

```
level-1 → cards            0 1px 2px rgba(0,0,0,.05)
level-2 → buttons, inputs  0 1px 3px + 0 1px 2px rgba(0,0,0,.1)
level-3 → modals           0 10px 15px + 0 4px 6px rgba(0,0,0,.1)
```

Modals are the only thing that get the big shadow, and they pair it
with the purple backdrop veil. Everything else stays close to the page.
No glow, no colored shadow, no hover-lift. The intent is a **paper-on-
desk** feel, not a material flight path.

## The shell

The app shell is canonical SaaS:

- **Left sidebar** (200px) on `#f5f6fc`. Sections stack with a light
  divider between them. Nav items are text buttons; the active item
  wears a `#ebecf6` pill and flips to purple Semi-Bold. A small
  **illustration promo card** sits near the bottom ("Invite others to
  co-manage your event") with a compact blue CTA. Below it, a single
  "My Events" link in brand purple.
- **Top bar** (56px) on white with a hairline bottom border. Left-aligned
  event title, a green "Published" pill, a blue "Preview" link. Right
  side carries the operational state: an amber "Services with minor
  issues" label with a small red dot, then the user avatar (40px,
  ringed in white).
- **Canvas** on `#e8e8ed`. All primary content sits in white cards
  (8px radius, level-1 shadow) with 24px padding.

## Forms inside the console

Form fields here are **completely different** from the guest form:

- Inputs are **36px tall** with 8/12 padding and a 6px radius.
- The border is an almost-invisible 1px inset in `#ebecf6` — the field
  is implied by its fill against the card, not drawn.
- On focus, the inset ring promotes to a 2px blue (`#3d91ff`).
- Placeholders are `#a5a5ac`, never meaningful copy.

Time inputs go a step further and drop the box altogether: just a
faint underline, with the placeholder "hh:mm" sitting on a baseline.
This keeps modals feeling airy, because time pickers tend to appear in
pairs (Starts at / Ends at) and boxed versions would feel caged.

The **toggle** pattern ("I'm not sure yet") uses a 36×20 pill:
off-state track is `#d8d8e3`, on-state is brand purple, thumb is a
16px white circle with level-2 shadow.

## Modals

Modals are the star pattern of this surface. The recipe:

1. Backdrop at `rgba(25,18,54,0.5)` — brand purple at half opacity,
   not black. This tints the world purple while you're focused.
2. White card, 624px wide, 8px radius, level-3 shadow.
3. Header: `Modal title` (18 Semi-Bold) with a 14 muted subtitle
   underneath. Both sit flush-left with 20/24 padding.
4. A hairline divider (`#e1e1e1`) under the header *and* above the
   footer. These divide the modal into three zones (header / body /
   actions) without visually fragmenting the card.
5. Body: 20/24 padding, fields stacked at 16px row gap.
6. Footer: Cancel floats left as a ghost button; "+ Save & add another"
   + "Save" pair to the right. Save is the only filled button on the
   whole surface.

## Buttons

Three flavors cover the whole system:

- **Primary purple** — brand.primary fill, white label, 8px radius,
  level-2 shadow. The only button that *commits*: Save, Build your
  Agenda.
- **Blue** — accent.blue fill, used for read-only or invitation
  actions: Preview, Invite Team Members. Smaller (32px), 6px radius.
- **Ghost text** — no fill, no border, brand-body color. Used for
  Cancel, add-another, and inline options.

Disabled state for the purple button slides to `#b5a9c4` — the same
hue, desaturated, so it still reads as "this is the Save button" but
obviously inert.

## Badges

Status badges live on the top bar and inline. They're always pill-shaped
(`100px` radius), 12px Semi-Bold, with a colored foreground on a very
pale matching fill. "Published" is the reference implementation:
`#09a96f` on `#d9f2e9`. Error and warning badges use the same shape
with their own color pairs.

## Illustrations and humans

The promo card in the sidebar carries a **colored illustration** of
two people collaborating at a laptop, contained in a 16px-radius card.
That's the one place real imagery appears. Everywhere else, visuals
are flat icons (Font Awesome 6 Pro, muted `#5e5972`) and text. The
illustration is deliberately tall and warm — it's meant to read as a
**human moment** inside what is otherwise a tool.

## Motion

Fast, short, eased. Field focus rings appear in 120ms, modals enter in
180ms with a small upward lift, the toggle thumb slides in 180ms.
Nothing bounces. The interaction language is "immediate and precise"
— appropriate for an operator clicking the same control hundreds of
times.

## What this system is *not*

- It is **not** the guest form. Do not reuse Arial, black hairlines, or
  flat-white sections. Those belong to the public surface.
- It is **not** a marketing site. There are no hero headlines, no
  gradients, no dark mode landing cards.
- It is **not** Material or iOS-native. Avoid raised floating buttons,
  bottom sheets, or depth inflation. One shadow per surface is enough.

The identity of this console lives in three choices: **purple for
commitment, blue for exploration, and restraint in everything else.**
