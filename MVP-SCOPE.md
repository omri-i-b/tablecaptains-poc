# Delegated Group Guest Management — MVP scope

> Internal product brief · Draft · Last updated 2026-05-12

## Executive summary

We're building a system for organizers to **hand off ownership of a chunk of their guest list to another person, and then keep operational oversight of that person's work without being in the middle of every change.**

We've prototyped this in two phases (v1, then v2) and have customer validation from two distinct shapes of the problem: Team Rubicon's mainstream sponsorship-driven gala (Nola Julian) and FMM's free-attend cultivation event (Jason Lee, Jim Dempsey). Team Rubicon is the broader signal — their operational shape recurs across thousands of nonprofit galas, hospitality programs, donor events, and corporate sponsorships.

The MVP is anchored on **Team Rubicon's shape** because it's the volume case. FMM-style edge behaviors (no-payment, fluid capacity, plus-one allowances) inform the data model but aren't on the MVP critical path.

**The bet:** RSVPify currently owns registration truth for events but loses the planner once delegation begins. Today they manage that next phase in spreadsheets, email chains, and Miro boards. We want to be the system of truth for that whole middle layer — from sponsorship sold through finalized guest list, ready for check-in.

---

## The actual problem

The customer's pain isn't registration. It's not seating. It's not communication. It's **distributed guest ownership over time, with operational fragmentation as the natural outcome.**

A sponsor commits to a table six months out. They don't know who they'll bring. The organizer spends the next six months chasing names, dietary needs, accessibility requests, and seat-swap requests through a tangle of emails, texts, verbal confirmations, and assistant hand-offs. The guest list isn't final until 48 hours before the event — sometimes 48 minutes before.

This breaks down operationally because:
- Organizers are forced to manually manage guests they don't directly control
- Real-world guest confirmations happen via texts, calls, and assistants — not self-service forms
- Guest lists evolve continuously: late adds, swaps, dietary updates, cancelations
- The seating chart, catering count, badge prep, and check-in queue all depend on data that's actively changing

**The job to be done:**

> Let me delegate ownership and management of a subset of my guest list to a responsible party without losing visibility, without losing operational control, and without forcing them or their guests into a rigid self-service flow.

This is what we're building. Not "table captains." That's RSVPify's marketing term for one slice of the system.

---

## Why "Table Captains" undersells what we're building

Internally we should think and architect around **Delegated Group Guest Management** because the same primitive applies cleanly across many use cases beyond nonprofit gala tables:

| Use case | Delegated owner |
|---|---|
| Gala sponsorship | Sponsor representative / table host |
| Golf foursome | Team captain |
| Hospitality suite | Suite lead |
| VIP pod | Executive host |
| Conference invite block | Producer / agency contact |
| Brand activation | Market lead |
| University donor table | Board member |
| Sales-team enterprise event | Account exec |

Externally we keep using customer-friendly language — "Table Host," "Table Captain," "Group Host" — because customers immediately understand those. The architecture under it is the reusable layer.

---

## Customer validation evidence

### Team Rubicon · Nola Julian
Senior development ops at Team Rubicon. Plans the Salute to Service gala (Nov 12, NYC). Sponsorships range $15K–$500K. Most payment offline via wire/check; credit card uncommon at these dollar levels. Older donor demographic, **email-only — "send me an email like an adult"** (her founder's phrase, used unironically).

Key things Nola validated in the May 15 walkthrough:
- The basic shape of the system (sponsor checkout → host portal → organizer dashboard) is right.
- **Plus-one max should be 1**, not N. If a host needs more, they send a separate invite.
- The host filling out the form is often **not the person attending** — EAs / PAs are the common pattern. The host *role* and the host *seat* are separate concepts.
- **Released seats are real** — paid-for-but-unused seats need to be "donated back" to the org as a distinct state, not silently sit as empty.
- Invoice ops aren't ready for automation — she wants an alert when someone requests one, then she creates and sends it manually from their CRM (DMS, via Microsoft).
- **Light branding is non-negotiable** — at minimum the org logo at the top of guest-facing pages. Ideally color + background image + font picker. Not custom CSS.
- Seating chart is currently Miro. She wants it integrated eventually, but not now.
- Day-of: she wants to hold credit cards on file for night-of charges (paddle raise, wine pull). That's a pre-authorization problem we're not solving in MVP.

### FMM · Jason Lee, Jim Dempsey
Run a fundraising masterminds program teaching nonprofits the "perfect vision dinner" model. Free-attend cultivation events. 60–80 captains recruited, expecting 50% to underperform, consolidation in the final week. **No payment in this flow.** Plus-ones not relevant (different lifecycle).

What FMM informed (but doesn't drive MVP scope):
- Coordinator-driven bulk captain entry is the realistic path — not self-service.
- Consolidation Tetris (merging undersized groups in the final week) is its own workflow layer.
- Live check-in iPad app is critical for them; out of MVP scope.

**Strategic call**: TR is the mainstream signal. We build for them. FMM stays in conversation; we don't bend the architecture to fit their edge cases yet.

---

## Conceptual model

These are the abstractions everything else is built on. Use these terms precisely in code, copy, and docs.

### Sponsorship
A purchase or commitment that entitles the buyer to a defined block of seats. Sponsorships are paid (card or invoice) or comped (organizer-created). A sponsorship creates exactly **one group**. Sponsorships have tiers (e.g., Patron $10K · 10 seats); each tier has a price and a seat count.

### Group
The operational guest list owned by a single host. A group has a name, a host, a capacity, and a roster of slots. The group is the unit of delegation — what the organizer hands off. Multiple groups can have the same host (one person managing more than one).

### Slot
A unit of capacity inside a group. A slot is always in one of these states:
- **Empty** — no guest assigned, the host can fill it
- **Awaiting response** — invited by email, no RSVP back yet
- **Confirmed** — guest filled in their info or host added them directly
- **Released** — donated back to the org, not available for the host to fill, paid for and counts as a comped seat for the organizer to redeploy
- **Declined** — invited guest said no (slot reverts to empty)

### Guest
A human in a slot. Has name, email, optional phone, optional title + organization, dietary preferences, dietary notes, accessibility needs, and a connection-to-cause note. May be part of a **party** (linked to another guest who came with them).

### Host
The human who owns and operates a group. **Host is a role, not a seat.** A host may or may not occupy a slot in their own group. A host can be reassigned by the organizer (e.g., EA replaces themselves with the CEO; one board member assumes ownership of three sponsor groups).

### Party
A grouping primitive that says "these guests came together; don't separate them at seating." Used for spouses, plus-ones, families. Indivisible.

### Released seats
A paid-for capacity that a host gives back. **They count toward overall sponsorship dollars but not toward the host's fill obligation.** The organizer can redeploy them as comped seats — typically into a virtual "Released to [Org Name]" group that absorbs unused sponsorship capacity.

---

## Personas

### Organizer / Planner
**Owns the event.** Creates sponsorships, sets pricing, configures branding, monitors group progress, intervenes when hosts go silent. Wants a **single dashboard** showing the room at a glance with the ability to drill in. Examples: Nola at Team Rubicon, a development director, an events coordinator.

Key needs:
- Cross-group visibility (completion %, who's behind, dietary/access counts)
- Light operational controls: add a group, reassign a host, mark paid/unpaid, archive a group
- Bulk import of hosts from a spreadsheet
- Composable follow-up emails to chase laggards
- Override capability — can edit any guest, any group, anytime
- Private notes that the host can't see (wealth capacity, donation history, "back for first time")

### Host / Sponsor / Table Captain
**Owns a chunk of the guest list.** Invites, adds, edits, replaces guests. Examples: a sponsor's primary contact, a board member, a corporate EA.

Key needs:
- A simple operational dashboard for their group(s)
- Both invite-by-email and add-directly entry paths
- Visual clarity: what's done, what's awaiting them, what still needs their attention
- Edit a customizable invite email (subject + body, with merge variables)
- Reminder nudges for guests who haven't RSVPed
- Release seats they won't fill
- Move guests between their own groups (if they own multiple)

### EA / Delegate
**Operates on behalf of the host.** May or may not attend. Often the realistic person filling out the form for a CEO or board member.

Key needs:
- All host capabilities
- Ability to keep the actual attendee informed via email but not as the primary contact
- Doesn't necessarily occupy a seat in the group they manage

### Guest
**The human being invited.** Older skew for donor events. Email-only communication. Expects light friction. Just wants to confirm and signal any dietary/accessibility needs.

Key needs:
- Clear who invited them, what the event is, when, where
- One-click confirm
- One-click decline (currently missing)
- Optional plus-one (max 1)
- Capture dietary, accessibility, title, organization
- Optional connection-to-cause note

---

## The lifecycle this product supports

This is the multi-phase reality of how a delegated guest list actually evolves. The product needs to support each phase explicitly.

### Phase 1 · Sponsorship sold (T-9 to T-6 months)
A sponsor commits via either credit card or an invoice request. They become a host of a new group. They don't yet know who they're bringing.

**Product:** sponsor checkout, invoice-request alerts to organizer, group auto-created on commit, welcome email to host.

### Phase 2 · Delegation (T-6 to T-3 months)
The host gets portal access. May ignore it for weeks. Organizer is building the early picture: which groups are active, which haven't logged in, which need a personal nudge.

**Product:** host portal, organizer overview with last-activity signals, follow-up email composer with per-host merge variables.

### Phase 3 · Progressive guest collection (T-3 months to T-2 weeks)
Hosts start inviting. Guests trickle in. Names get added, dietary needs captured, plus-ones declared. State is fluid — a host might invite five, get three confirms, two declines, then send three more invites.

**Product:** all host management features. Editable invite templates. Replace-guest flow. Move-between-own-tables. Reminder nudges. Guest RSVP form with cannot-attend, dietary, accessibility, title/org.

### Phase 4 · Chase and finalize (T-2 weeks to T-1 week)
Organizer sees who's underperforming and chases. Some hosts release unused seats. Walk-up adds. Last-minute swaps. EA-driven additions for executive teams.

**Product:** organizer cross-group dashboard. Released-seat flow. Add-guest-anywhere from organizer side. Reassign host. Custom reminder emails to specific hosts.

### Phase 5 · Operational readiness (T-1 week to T-0)
Cutoff hits. Final headcount sent to venue, catering, AV. Dietary and accessibility reports printed. Badge prep starts.

**Product:** lock guest editing post-cutoff (configurable). Final-headcount stat. Dietary/accessibility totals. CSV exports for catering and venue.

### Phase 6 · Event day-of (T-0)
Existing RSVPify check-in handles arrival. Out of MVP scope.

---

## What MVP includes

Organized by surface. Each item tagged with priority:
- **P0** = ship blocker
- **P1** = strong yes for MVP, can defer 1-2 if engineering forces a cut
- **P2** = nice-to-have, fold in if time

### Sponsor checkout (`captain-purchase.html`)

| Item | Priority | Evidence |
|---|---|---|
| Tier picker with 4–6 sponsorship levels, name + price + seat count + perks | P0 | TR uses 5–6 tiers |
| Multi-quantity within tier (cap at low number, de-emphasized) | P1 | Nola: uncommon but useful |
| Host details (name, email, org, phone, group name) | P0 | — |
| Payment method choice: pay-by-card *or* request-invoice | P0 | TR + FMM both have offline payment |
| Invoice recipient selector when "request invoice" is chosen (self / different recipient with name + email) | P0 | Nola: registrant often ≠ bill-payer |
| Invoice-request alert to organizer (not auto-invoice) | P0 | Nola: she sends invoices manually from DMS |
| G&S tax-deductible amount on receipt/invoice (not on checkout page) | P1 | Nola: needs to be on receipt |
| Light event branding on this surface (logo, color, font) | P1 | Nola: non-negotiable eventually |
| "Sponsorships" copy throughout (not "tables") | P0 | Nola: external customer language |
| Success state with link to host portal | P0 | — |

### Guest RSVP form (`guest-rsvp.html`)

| Item | Priority | Evidence |
|---|---|---|
| Pre-filled email from invite link | P0 | — |
| Full name, phone (optional) | P0 | — |
| **Title and organization (optional)** | P0 | Nola: pre-vetting which tables have which-level execs |
| Dietary chips (vegetarian, vegan, GF, etc.) + custom allergy notes | P0 | — |
| Accessibility needs free-text | P0 | — |
| **"Cannot attend" decline button** with optional reason, sends regret to host | P0 | Nola: biggest miss in walkthrough |
| Plus-one binary (yes / no, max 1) | P0 | Nola: max 1; host sends separate invite if more |
| Connection-to-cause optional note | P1 | Carries over from FMM model; broadly useful |
| Confirmation success state | P0 | — |
| Light event branding (logo + color + background) | P1 | Nola: non-negotiable |

### Host portal (`captain-portal.html`)

| Item | Priority | Evidence |
|---|---|---|
| Multi-group switcher (if host owns more than one) | P0 | Common: one person managing multiple sponsorships |
| Editable group name | P0 | Nola: host calls it different things than organizer |
| Slot-based roster with three visual states (confirmed / awaiting / empty) | P0 | — |
| Strong visual distinction between awaiting and empty slots | P0 | Nola wording: "still need" vs "awaiting response" |
| Invite by email with editable subject + body, merge vars, live preview | P0 | Nola: "very commonly requested" |
| Add guest directly (manual entry) | P0 | EA workflow |
| Edit guest (name, email, phone, dietary, accessibility, private host note) | P0 | — |
| Replace guest workflow (swap name, keep slot) | P0 | Nola: "happens in life" |
| Move guest between host's own groups | P0 | Nola: explicitly called out |
| **Release seats** flow (per-group "release remaining" + per-seat) — donates back, locks add-guest | P0 | Nola: critical, distinct third state |
| Reminder nudge for guests who haven't responded | P1 | — |
| Visible "from" email address with edit option | P1 | Missy: hosts want their email visible to guests |
| Dietary + accessibility chips on roster | P0 | — |
| Plus-one indicator on roster (with who) | P1 | Nola: missing in current build |

### Organizer overview (`organizer-overview.html`)

| Item | Priority | Evidence |
|---|---|---|
| Cross-group dashboard: groups list with host, fill bar, status pill | P0 | — |
| Top-line stats: groups, confirmed, awaiting, still-needed, **total seats sold** (renamed from "final headcount") | P0 | Nola: confused by current "final headcount" wording |
| Cutoff urgency banner (escalates by days remaining) | P0 | — |
| Filter pills: All / Complete / In progress / Needs attention | P0 | — |
| Search by host or group name | P0 | — |
| Side drawer per group: roster, activity log, edit any guest, reassign host, archive group | P0 | Nola: "I would have privileges to adjust any of these" |
| Custom follow-up email composer with merge vars, sent to one or many hosts | P0 | — |
| Bulk host import (CSV-style paste) | P0 | Nola: side-load hosts who didn't go through checkout |
| Add new group manually (no invoice, e.g. comped staff table) | P0 | Nola: staff prospect table for new business officer |
| Add guest directly into any group | P0 | — |
| Reassign host on a group | P0 | Nola: critical for EA / one-person-many-tables case |
| Archive group | P1 | — |
| **Paid / unpaid marker** per group (visual toggle, no payment ops here) | P0 | Nola: source of truth in DMS, but useful marker |
| **Released seats accounting** — virtual "Released to [Org]" group or separate counter | P0 | Nola: distinct state |

### All guests view (`organizer-guests.html`)

| Item | Priority | Evidence |
|---|---|---|
| Flat searchable list across every group | P0 | — |
| Type filter (host / guest) | P0 | — |
| Pending / dietary / accessibility filters | P0 | — |
| Click row → edit guest modal (organizer override) | P0 | — |
| Replace guest | P0 | — |
| Move guest to different group (organizer override) | P0 | — |
| **Private organizer notes** (hidden from host) — wealth capacity, donation history, etc. | P0 | Nola: critical for seating |
| Paired-guest indicator showing **who** they're paired with | P0 | Nola: missing reveal; just shows the icon |
| CSV export | P0 | — |

### Branding (cross-cutting)

| Item | Priority | Evidence |
|---|---|---|
| Logo upload | P0 | Nola: minimum |
| Primary color | P1 | Nola: "I can just type in our colors" |
| Secondary color / accent | P1 | — |
| Background image option | P2 | Nola: "primo level" |
| Font picker (3–5 web-safe options) | P2 | Nola: deferred OK |

### Confirmation emails (new surface, not yet built)

| Item | Priority | Evidence |
|---|---|---|
| Editable confirmation email template | P0 | Nola: explicitly asked |
| Progressive content support (different content at different points pre-event) | P1 | Nola: dress code early, auction items late |
| Merge variables: guest name, host name, table name, event details, parking, dress code, schedule link, auction link | P0 | — |
| Preview before send | P0 | — |

---

## What MVP does NOT include

Each of these is a thing customers asked for. We have a reason for each cut.

### Seating chart / spatial orchestration
**Why out:** Nola uses Miro today and accepts it stays separate for MVP. This is its own multi-month engineering effort. Future expansion area, not MVP.

### Live day-of check-in (iPad / restaurant-style)
**Why out:** Existing RSVPify check-in flow handles arrival. FMM asked for it; not MVP for TR.

### Night-of credit card hold for paddle raise / wine pull
**Why out:** Pre-authorization problem with their current CRM (DMS). Genuinely hard and they don't expect us to solve it in MVP. Separate workstream if we want to.

### Deep CRM integration (Microsoft DMS, QuickBooks, NetSuite)
**Why out:** Nola explicitly said paid/unpaid is a light marker; source of truth stays in DMS. Two-way sync is a Phase 2 conversation.

### Auto-generated invoice PDFs
**Why out:** Nola sends invoices manually from her CRM. She wants a notification trigger, not an automation. We're solving the right problem with a smaller scope.

### Donation add-ons during RSVP (e.g., "sponsor a volunteer hour for $36")
**Why out:** Interesting expansion area; not core to delegation problem.

### Plus-N (more than 1 plus-one per invitee)
**Why out:** Nola: max 1. If host needs more, they send another invite. Forces clean accounting.

### Fundraising attribution / donor scoring / peer-to-peer
**Why out:** FMM territory. Separate product layer. Not where TR or the mainstream is.

### Multi-language guest forms
**Why out:** No explicit ask yet. Defer.

### Mobile-native apps
**Why out:** Responsive web is sufficient for both surfaces. Host portal especially is desktop-skewed (organizers and EAs at computers).

---

## Success criteria

MVP is "shipped" when:

1. **Team Rubicon uses it for Salute to Service 2026** (November 12, NYC), end-to-end, from first sponsorship through final guest list handed to check-in.
2. Nola can complete the following without contacting RSVPify support:
   - Onboard 30 sponsorships across 6 tiers
   - Pull a CSV of all guests with dietary + accessibility two weeks before event
   - Reassign a host on a sponsor group
   - Release seats from a sponsor who under-fills, redeploy them as comped
3. Average host completes their group fill **without contacting Nola** for at least 80% of action types (invite, add, edit, replace, release).
4. We have at least one second customer in a similar shape (nonprofit gala $1M+ event revenue) signed for the next cohort.
5. **Zero hand-management of guest data in Google Sheets** for the events that use the system.

---

## Open product questions

These need decisions before or during the build:

1. **How does the host portal land?** Email link with magic token, or password + login? TR's demographic is email-driven; magic links are friendlier but have security implications.
2. **What's the data model for "Released to TR"?** A real virtual group with comped seats, or just an organizer-side counter? Affects how the organizer assigns guests to those seats later.
3. **Single host per table — do we enforce or just default?** A group has one host of record. EA-driven flows mean the host of record may not be the seated person. The host's *seat* is just one row in their group like any other.
4. **Invoice recipient — does it persist?** If the same EA fills multiple sponsorships, do we remember their preference? Probably not for MVP — keep it per-checkout.
5. **What's the cutoff lock policy?** After May 12 cutoff (TR example), do guest edits lock? Host edits? Organizer overrides anything? Need a clear policy.
6. **Branding scope — is this just for the guest RSVP and host portal, or sponsor checkout too?** Probably all three. Confirm with design.
7. **Bulk import — do hosts get a welcome email automatically when imported, or only when the organizer flips a switch?** Affects flow.
8. **Plus-one decline path** — if a guest brings a plus-one and the plus-one declines, does that free the slot or does it disappear with the primary? Probably the former.

---

## Risks

### Product
- **"Delegated guest management" is abstract.** Customers respond to "table captains." Marketing positioning needs to keep the customer language while engineering thinks in the abstract. Risk of customer copy and code drifting.
- **Released-seat accounting is novel.** No competitor has this. If we model it wrong (e.g., misleading fill percentages), it'll confuse hosts and organizers.
- **Light branding is a slippery slope.** Customers will ask for more. Need to draw the line cleanly at logo + color + background — and hold it.

### Technical
- **Magic-link auth** for host portals is the easiest experience but the riskiest security model. Need to scope token expiry, link revocation, and what happens if forwarded.
- **Email delivery from custom-branded "from" addresses** has DKIM/SPF implications. We probably end up sending from a RSVPify sender domain with a per-host reply-to. Verify with eng.
- **CSV bulk import** edge cases (Excel character encoding, smart quotes, multi-line cells) bite people every time. Budget time.
- **Editable email templates with merge variables** are surprisingly complex to ship safely (escaping, malformed templates, broken merges). Don't underestimate.

### Market / customer
- **TR alone isn't a market.** We need to validate at least one second customer (different nonprofit, similar gala shape) early in the build to derisk that the abstraction holds.
- **FMM is watching the same build.** If we ship a TR-shaped MVP and they react that it doesn't fit their model, we have to be ready to say "yes, here's where you fit in our roadmap" without conceding scope.

---

## Suggested sequencing

Three milestones, each shippable internally for review.

### M1 · Foundations (3–4 weeks)
- Sponsor checkout with invoice-recipient field, invoice alerts
- Guest RSVP form with cannot-attend, title/org, plus-one binary
- Host portal: groups, slots, invite/add/edit/replace/move, editable templates, reminders, released-seat flow
- Organizer overview: cross-group dashboard, drawer with editable roster, reassign host, paid/unpaid, headcount-renamed
- All guests view: search, filter, edit, private notes, paired-guest reveal, CSV export

### M2 · Onboarding readiness (2–3 weeks)
- Bulk host import
- Add-guest-anywhere from organizer side
- Add-comped-group from organizer side (no invoice)
- Light branding (logo + primary color)
- Confirmation email template editor
- Magic-link auth for host portal

### M3 · TR cohort launch (2–3 weeks)
- Walk TR through onboarding live
- Daily Slack channel for fast feedback
- Patch as we learn
- Second customer validation in parallel

**Total est: 7–10 weeks of focused engineering work**, plus design and product cycles.

---

## Glossary

| Term | Definition |
|---|---|
| **Sponsorship** | A purchased commitment that creates a group. Tier-priced. May be paid by card or invoice. |
| **Group** | An operational guest list owned by one host. Has capacity, name, roster. |
| **Slot** | A single position in a group's capacity. States: empty, awaiting, confirmed, released, declined. |
| **Host** | The human who manages a group. Role, not seat. Reassignable. |
| **Guest** | A human in a slot. |
| **Party** | A grouping of guests that cannot be split for seating. |
| **Released seat** | A paid-for slot a host has given back to the org. Counts toward dollars, not toward host obligation. |
| **Cutoff** | The date past which guest edits lock (configurable per event). |
| **Comped seat** | A free seat the organizer creates outside the sponsorship flow. Lives in a group like any other. |
| **Final / total seats sold** | The sum of capacity across all sponsorships sold, minus released. The number sent to venue and catering. |
| **Magic link** | A one-time URL emailed to a host that signs them into their portal without a password. |

---

## Open for input

This doc is a draft. Comments, pushback, edits welcome — especially on:
- The phase model (does it match how planners actually think?)
- The released-seat model (is the accounting right?)
- The sequencing (is M1 realistic?)
- Out-of-scope items (anything we should pull back in?)

Owner: Omri Buzi (Product)
