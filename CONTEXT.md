# Table Captains POC — context dump

A running record of what was built, why, and what the April 28 FFM demo
told us to change. Drop this back into a future session for instant context.

---

## Where things live

- **POC live**: https://omrib.dev/tablecaptains-poc/
- **POC repo**: https://github.com/omri-i-b/tablecaptains-poc (public)
- **Local source**: `/Users/omri/code_projects/tablecaptains/`
- **Root domain repo**: https://github.com/omri-i-b/omri-i-b.github.io
  (just an index landing page + `CNAME` for `omrib.dev`)

---

## Hosting setup (so future-me doesn't re-derive this)

`omrib.dev` is a GitHub Pages user site:

- `omri-i-b/omri-i-b.github.io` owns the apex domain → serves `omrib.dev/`
  - Contains `index.html` and `CNAME` (`omrib.dev`)
- Any other repo on the `omri-i-b` account with Pages enabled auto-mounts
  at `omrib.dev/<repo>/` — no extra DNS, no extra `CNAME` file required.
  - `omri-i-b/tablecaptains-poc` → `omrib.dev/tablecaptains-poc/`

### Cloudflare DNS for omrib.dev (apex)
All records **DNS only (grey cloud)**, otherwise GitHub can't issue the
Let's Encrypt cert. Critical for `.dev` since `.dev` is HSTS-preloaded —
no HTTP fallback, cert must work day one.

| Type  | Name | Content                  | Proxy    |
|-------|------|--------------------------|----------|
| A     | @    | 185.199.108.153          | DNS only |
| A     | @    | 185.199.109.153          | DNS only |
| A     | @    | 185.199.110.153          | DNS only |
| A     | @    | 185.199.111.153          | DNS only |
| AAAA  | @    | 2606:50c0:8000::153      | DNS only |
| AAAA  | @    | 2606:50c0:8001::153      | DNS only |
| AAAA  | @    | 2606:50c0:8002::153      | DNS only |
| AAAA  | @    | 2606:50c0:8003::153      | DNS only |
| CNAME | www  | omri-i-b.github.io       | DNS only |

SSL/TLS mode: **Full** (not Flexible, not Off). "Always Use HTTPS" off at
Cloudflare level — let GitHub handle it.

---

## Pages built

All static HTML/CSS/JS. No build step. Each page is self-contained.

- `captain-purchase.html` — captain intake form (name, email, table name,
  connection-to-cause note, seat-count guess). Originally had package tiers
  + payment; both removed. Originally had a duplicate-email alert; removed.
- `captain-portal.html` — captain's guest-management view. Where the bulk
  of the work landed.
- `organizer-guests.html` — admin view of all captains and their guests.
- `organizer-packages.html` — was for tier setup; effectively obsolete given
  there are no tiers in this model.

---

## The conceptual model we were building toward

Wrote this up for the demo audience:

> Standard Table Captains is a **purchase flow**: captain buys a tier, gets
> a fixed-size table, fills it. This instance is a **recruitment-and-
> qualification flow**: captain promises to bring N people to a free,
> off-the-books cultivation event. There's no checkout, no tiers, no
> inventory. Money — if there is any — happens offline via invoice. The
> unit of value isn't a paid table; it's a captain's commitment to fill
> seats with the right prospects.

### What the captain does (as built)
1. **Reserve a table** — sign up, leave a connection-to-the-cause note,
   pick best-guess seat count.
2. **Recruit and qualify** — invite by email (with optional plus-one
   allowances per invitee) or add a guest directly. Each invitee writes
   their own connection note when they RSVP. Captain layers in private
   notes.
3. **Adjust as reality changes** — release seats they won't fill, or
   request more seats. Removing a guest also drops any plus-ones extended
   to them specifically.

### What the organizer does (as built)
1. **See the room as captains + guests** — type filter, captain column on
   guest rows, linked-guests indicator, top-line stats.
2. **Approve seat requests** — pending captain requests show inline on the
   relevant table; one click to approve (appends seats) or deny.
3. **Add tables and guests directly** — back-fill captains, walk-ins, etc.
   Rename tables (captain's "Acme Co." vs. planner's "Table 4").

### What's gone vs. standard TC
Payment, package tiers, dietary as a top-level field, share-a-link
(everything goes through email invites the captain can preview Luma-style).
Meal hidden by default — moved to detail drawer.

---

## Implementation notes worth remembering

### Plus-ones in the captain portal
- Each seat has a stable `id` (`s1`, `s2`, ...). Plus-ones link to their
  primary by `linkedToId`, **never** by array index — splicing rows out
  would otherwise corrupt other plus-one references.
- Status enum: `captain | confirmed | invited | open | released | plus-one`.
- When the primary is removed via Edit → Remove guest:
  - Primary's seat resets to `open` in place (keeps its id and slot).
  - Linked plus-one rows are spliced out entirely (the +1 was a courtesy
    extended to that specific guest — it goes when they go).
  - Surviving seats renumber sequentially.
- "Release this seat" is reserved for *empty* capacity. Filled seats use
  Edit → Remove guest. The detail-modal release button is hidden.

### Seat-request flow
- Captain saves request to `localStorage` under
  `tablecaptains.data.v1.captain.seatRequest = { amount, note,
  requestedAt, status: 'pending' }`.
- Captain portal shows a yellow banner with cancel option.
- Organizer view (currently hard-coded on the Acme table) shows a pill
  with inline Approve / Deny — Approve appends N new open seats to the
  table's `seats[]`, Deny clears the request.

### Connection-to-cause note
Editable when captain adds a guest manually (was readonly). Same field
shown to organizer in detail drawer.

---

## April 28 demo findings — what FFM (Jason / Jim) actually need

Recorded with full transcript context. The model we built is close in
spirit but **wrong in several specifics**. The actual model is simpler in
some ways and more complex in others.

### Things we got fundamentally wrong

1. **Captains don't self-serve.** Coordinator bulk-registers 60–80 table
   hosts up front; they receive an email with a portal link. The intake
   form is at most secondary, not primary.
2. **There is no seat count.** Their model is "bring as many as you can,
   no commitment, no minimum, no maximum." Strike the seat-count picker,
   release-seat, and request-more-seats affordances entirely.
3. **"Tables" don't exist for 95% of the lifecycle.** They're fluid groups
   until ~3 days before the event. Real tables only get assigned at the
   final consolidation pass.
4. **Parties, not just plus-ones.** Husband-wife, family-of-3, etc. —
   indivisible units that register together. Plus-one is a special case;
   the model is "party of N, never split."
5. **The most important view doesn't exist yet.** A consolidation Tetris
   board: each captain's group as a card with size + party breakdown,
   merge a group-of-4 into a group-of-6, reassign the displaced captain,
   then drop full groups onto physical tables.
6. **Day-of live check-in iPad app missing.** Restaurant-style table
   diagram, real-time hole visibility, captain check-in flow asks "anyone
   not coming?", walk-up "ungrouped" guests assigned to holes on the spot.
7. **No "ungrouped" bucket.** 5–10% of registrants come from mass-email
   signups without a captain. They're hidden from the venue count and
   absorb no-show holes day-of.

### Things we got right
- No payment anywhere ✓
- Linked guests / parties indicator (Jason explicitly called this out)
- Captain vs guest type filter
- Custom invite email with Luma-style preview
- Rename tables
- Per-guest connection-to-cause note (donor-qualification capture)
- Coordinator-driven entry path (add captain / guest / table directly)
- Open API + MCP + Salesforce/HubSpot integrations

### Build order for September
1. **Group + party data model** — drop the seat construct entirely.
2. **Bulk captain registration** — coordinator imports/creates many at once.
3. **Consolidation Tetris view** — merge small groups, reassign table-hosts,
   captain-performance at a glance.
4. **Live check-in iPad app** — table diagram with holes, no-show capture,
   walk-up assignment from ungrouped.
5. **Underperforming-captain dashboard** — group-size-sorted, so the
   calling team knows who to dial today.
6. **Fully customizable email templates** — already a strength.
7. **Pre/post-event lifecycle hooks** — name-storming, gift counting,
   thank-yous (currently Google Sheets).
8. **CRM-adjacency / follow-up nurture** — events are the front door;
   donor cultivation is the bigger play.

### Things to delete from the current POC
- Captain self-purchase form (or demote heavily)
- Seat-count picker on intake
- "Best guess at how many seats" prompt in the portal
- Release seat
- Request more seats + organizer approve/deny
- Seat numbering in captain portal (no `Seat 7` column)

### Timeline & commercial posture
- **May event**: not us. They're not redoing course materials in two weeks.
- **September cohort**: target. They redo videos + workbook around our
  product if we land it.
- **Now → September**: Brent's framing — sit shotgun through the May cohort,
  listen + learn, prioritize sprint work against observed reality.
- **Gate**: contractual commitment unlocks roadmap prioritization. Jason
  open; Jim's bar is "must be confident enough to recommend to 160 NPOs."
- **Risk**: Jason was hoping we'd say "we have everything you need today."
  We didn't. Real runway, but a runway — not a green field.

---

## Useful commands

```bash
# View deployed Pages status
gh api /repos/omri-i-b/tablecaptains-poc/pages
gh api /repos/omri-i-b/omri-i-b.github.io/pages

# Verify cert + DNS
dig +short omrib.dev A
echo | openssl s_client -connect omrib.dev:443 -servername omrib.dev 2>&1 | grep -E "(subject|issuer)"

# Re-trigger cert issuance if it stalls
gh api -X PUT /repos/omri-i-b/omri-i-b.github.io/pages -f cname=
sleep 5
gh api -X PUT /repos/omri-i-b/omri-i-b.github.io/pages -f cname=omrib.dev
```
