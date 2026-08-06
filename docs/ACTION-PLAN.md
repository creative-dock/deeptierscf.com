# Feedback action plan — consolidated

Sources: **A** = Ales (Loom review, transcribed to task spec), **O** = Oscar (written section-by-section walkthrough), **BOTH** = agreed.

Coverage: Ales covers `index.html`, `tier-2.html` and `anchors.html`, plus a general complexity flag on `anchors.html` + `tier-1.html`. He gives **no line-item feedback on `tier-1.html`** (he trailed off; a "Part 4" may exist) and **nothing at all on `how-it-works.html`** — that page is Oscar-only.

Status legend: **READY** = decided, can be implemented now. **DEFERRED** = parked pending a conversation, off the critical path. Items marked **DECIDED (Qn)** record a conflict between the two reviewers and how it was resolved; the full decision log is §7.

**All 14 open questions were resolved on 2026-08-06.** Everything is READY except W11 (FAQ question set to be drafted for review first) and A6 (deferred). Two new global constraints came out of that round: G1b (wordmark) and G11 (no AI claims).

---

## 1. Global rules (apply to every page)

| ID | Change | Source | Status |
|---|---|---|---|
| G1 | Remove em dashes and en dashes **as punctuation** site-wide. Replace with semicolons, colons, commas, full stops or parentheses. **Hyphens in compound words stay** ("deep-tier", "high-street", "investment-grade"). **DECIDED (Q1).** | O | READY |
| G1c | **Check every dash form, not just `&mdash;`/`&ndash;` entities.** A first pass on this missed literal Unicode `—` (U+2014) surviving in all five `<title>` tags and in HTML/CSS/JS comments, because the check only grepped for the named entities. The audit must cover: literal `‒ – — ―`, named entities, numeric entities (`&#8212;`, `&#8211;`), and a spaced hyphen used as a dash (` - `). Titles now use a colon between name and descriptor. The FAQ collapse glyph was an en dash and is now a true minus sign (`\2212`), which is the correct character for that job anyway. | User | READY |
| G1b | The wordmark is **deeptier**, one word. Use it whenever referring to the product or the solution as an entity. **DECIDED (Q1).** | User | READY |
| G2 | Cap sentences at 20–30 words. Prefer bullets over paragraphs. If a line repeats something said elsewhere, delete it rather than rephrase it. | BOTH (A principle_1) | READY |
| G3 | Stop using "program"/"programme" to describe **our** solution; it gets confused with conventional SCF programs. Keep it only when describing the legacy alternative we contrast against (e.g. "no programme to join" stays). | O | READY |
| G4 | **"Story" is split by position, not banned. DECIDED (Q2):** out of every hero and section headline (H1/H2), where it must be **"verified transaction record"**; allowed to stay in body copy, step titles and FAQ answers where it genuinely aids the explanation. This honours Oscar's objection at the points of highest visibility and Ales' view that the framing itself is good. Audit list in §1.1. | BOTH + user | READY |
| G11 | **No AI claims anywhere.** There is little to no AI in the funding process; the only real use is document data ingestion. The site currently makes **zero** AI claims — keep it that way. This is a guardrail for the new copy, especially the FAQ rebuild (W11) and the verification sections, where "AI-powered verification" would be an easy and wrong reach. Verification is evidence-based and independent, not algorithmic. | User | READY |
| G5 | Remove the `logo tbd` chip in the header; keep the wordmark only. | O | READY |
| G6 | Remove the rounded pill tag at the top of every page (`Deep-tier supply chain finance — tier 2 and beyond`, `For OEMs & anchor buyers`, `For tier 1 suppliers`, `For tier 2 suppliers and beyond`, `The mechanics`). The page already says where you are. Review whether any pill/chip is worth keeping. | O | READY |
| G7 | Push all step-by-step mechanics (PO/invoice matching, verification sequence) to `how-it-works.html`. Role pages lead with benefit, not process. | A principle_2 | READY |
| G8 | Lead every page with benefit-first messaging (fairness, speed, visibility, resilience) before tier-segmented or technical detail. | A principle_4 | READY |
| G9 | Any table or diagram must be visually tied to the copy next to it, never floating as a separate element. | A principle_3 | READY |
| G10 | Plan A/B testing of hero headline variants with real clients in interviews before locking copy. | A principle_6 + O closing note | Not a code task |

### 1.1 "Story" audit — every occurrence, with the G4 verdict

13 occurrences across 4 files. `tier-1.html` has none.

| Location | Context | Verdict |
|---|---|---|
| `index.html:184` (×2) | Solution H2: "We build the **story** that connects the invoice to the anchor … the funder lends against the **story**." | **Replace both.** Section headline. The highest-visibility use and the one Oscar objected to by name. |
| `index.html:327` | CTA H2: "Bring us one chain. We'll show you the **story** inside it." | **Replace** (headline). Note: Oscar praised this line as catchy, so it needs a careful rewrite rather than a find-and-replace. Flagged in B3. |
| `how-it-works.html:39` | Hero H1: "A **story** a funder can underwrite." | **Replace.** Hero. Also covered by W2. |
| `index.html:83` | Hero diagram footer: "**Verified story:** invoice → PO → PO → anchor demand" | **Moot** — H4 deletes this footer entirely. |
| `tier-2.html:251` | Step H3: "We verify the **story** upward" | **Keep.** Mid-explanation step title, exactly the case Q2 allows. |
| `how-it-works.html:143` | Step H3: "We assemble and verify the **story**" | **Keep.** Same reasoning. |
| `how-it-works.html:338` | FAQ answer body | **Keep.** Body copy. |
| `anchors.html:220` | Body: "criticality analysis built from those verified **stories**" | **Keep**, but the plural reads awkwardly; consider "verified transaction records" here. |
| `index.html:7`, `tier-2.html:7` | `<meta name="description">` | **Replace.** Meta descriptions are search-result headlines, so treat them as hero copy. |

---

## 2. `index.html` (Overview / homepage)

### 2.1 Hero

| ID | Change | Source | Status |
|---|---|---|---|
| H1 | Rewrite H1. Current: "Working capital that reaches the tiers your program never touches." New message: we deliver **direct financing to deeper tiers, without exposing anyone's balance sheet and without a rigid financing programme**. Must not pre-suppose which tier the reader is. | BOTH | READY |
| H2 | Rewrite the lead paragraph. Points to make, in order: (1) we finance **transactions**; (2) a transaction starts with an invoice; (3) we reconnect the surrounding data to make that transaction reliable to a funder. Short. | O | READY |
| H3 | Remove the pill above the H1. | O | READY (= G6) |
| H4 | Simplify the hero diagram (`.tierstack`). **Keep** the three-node relationship (Anchor → Tier 1 → Tier 2+) and keep Tier 2 highlighted. **Remove** the PO numbers, invoice numbers and the "purchase order" edge labels; we're not going into that detail here. **Remove** the whole `Verified story: invoice → PO → PO → anchor demand` footer. | O | READY |
| H5 | The 4-item strip (`Tier 2+` / `Zero` / `Per invoice` / `ERP native`) carries little information and reads as repetition. **DECIDED (Q5): consolidate into one line inside the hero.** Removes the disconnected-from-copy defect Ales flagged and the low-information labels Oscar flagged, in one move. | BOTH | READY |

### 2.2 Section 01 — The problem

| ID | Change | Source | Status |
|---|---|---|---|
H6 | Rewrite the whole section around Oscar's actual problem statement: **tier 2+ companies can't get the financing terms that anchors and tier 1s get.** Because: they're often unrated; they have no direct commercial relationship with the anchor; so funding programmes don't cover them; so they go to commercial banks at higher rates, or their credit limit is smaller than the POs the anchor's demand generates. | O | READY |
| H7 | Keep the H2 "Liquidity stops at tier 1. The risk doesn't." but tighten it slightly. | A | READY |
| H8 | Convert all three problem cards from paragraphs to short bullets. Currently "no one is going to read it." | A (high confidence) | READY |
| H9 | "The gap in one sentence" callout. **DECIDED (Q6): keep it, split into two short sentences.** Ales called it dense, Oscar called it really good; splitting preserves the meaning Oscar liked and fixes the density Ales objected to. Retitle if it's no longer one sentence. | BOTH | READY |
| H10 | The 4-item `×` list ("Not a receivables sale" etc.): redesign as a compact table or a list under a header such as "The issues"; drop the trailing explanations. | O (A concurs vaguely) | READY |

### 2.3 Section 02 — The solution

| ID | Change | Source | Status |
|---|---|---|---|
| H11 | Reframe the H2 "We build the story that connects the invoice to the anchor…". The **insight is right** and both reviewers say keep the framing; both instances of "story" must go, per G4 (headline position). | BOTH | READY |
| H12 | Cut the supporting paragraph ("Instead of a program, we assemble evidence…") to roughly one line. The ERP/PO mechanics move to How it works. | BOTH | READY |
| H13 | The 3-node flow (`Demand originates` / `Demand cascades` / `The financeable event`). **DECIDED (Q3): remove from the homepage.** The cascade now lives in exactly one place, `how-it-works.html` (W5), which already carries its own version. Oscar's two fixes for it (one-line descriptions, and the cramped gap between the chip and the node title) **carry over to W5** so nothing he asked for is lost. | A over O | READY |
| H14 | Of the three solution cards, **"Verification, not self-declaration"** is the one that earns its place now. Make it more prominent and fold it into the core solution statement; it's the best single illustration of what we do. | O | READY |
| H15 | "No program to stand up" and "Data flows both ways": both restate things said elsewhere. Cut or demote. | O | READY |

### 2.4 Section 03 — What you get / Three positions in the chain

| ID | Change | Source | Status |
|---|---|---|---|
| H16 | Content is right but far too long. Reduce each of the three cards to **one impact statement** (each role has its own landing page for the detail). | BOTH | READY |
| H17 | Move this section **higher up the page**, above the solution block. **DECIDED (Q4): yes.** With the flow diagram gone (H13), this is #2 on Ales' own priority list. | A | READY |
| H18 | Anchor/OEM card: lead on **risk signals and visibility**. Suggested framing from Oscar: *"see the smoke before the fire"* — risk signals that stop a supply chain failure becoming millions in delay costs. | O | READY |
| H19 | Tier 1 card: lead on **comfort**. The funder puts money into their suppliers without tier 1 exposing its balance sheet; better standing with the anchor; assurance that tier 2+ have the cash to produce. | O | READY |
| H20 | Tier 2+ card: lead on **access to better rates**, because an explicit, evidenced relationship between the anchor and the tier 2 transaction lets them borrow against the chain's credit quality, not their own. | O | READY |

### 2.5 Final CTA

| ID | Change | Source | Status |
|---|---|---|---|
| H21 | Keep the catchy line "Bring us one chain. We'll show you the story inside it." — but it's an H2, so "story" goes (G4). Needs a careful rewrite that preserves the hook Oscar praised, not a mechanical substitution. | O | READY (copy pass, B3) |
| H22 | Rewrite the paragraph under it. It's currently inaccurate: this is **not an anchor programme**. It's a solution that funds tiers; and the more tier 2+ companies that use it, the better the visibility the anchors get. | O | READY |
| H23 | Make the CTAs role-agnostic, since at this point we don't know who's reading. Keep two buttons: broaden "Talk to us as an anchor" to **"anchor or tier 1"** (their approach to us is the same), and make the other one explicitly tier-2 flavoured, e.g. "Do you have a transaction to fund?" / "Are you interested in funding an invoice?" | O | READY |

---

## 3. `anchors.html` (OEM / Anchor)

| ID | Change | Source | Status |
|---|---|---|---|
| A1 | Remove the `For OEMs & anchor buyers` pill; we're already on that page. | O | READY |
| A2 | Hero H1: change "You underwrite the demand. / Now see who's actually building it" → the first half becomes **"you create/start the chain"** (anchors decide how much production goes into motion), and the second half must carry our real value proposition: **risk signals and visibility**. | O | READY |
| A3 | Hero-right "Deep-Tier Signal View" table (Precision castings / Machine shop / Surface treatment / Fasteners, tagged Healthy / Strained / Watch). **Ales: the table itself is good** — a useful red-flag mechanism and a genuine anchor benefit. **Keep the concept.** Refine it per Oscar: make it obviously a **health dashboard of the deeper supply chain**, strip the repeated "program" wording (G3), and delete the "signals are derived from verified…" footnote. | BOTH | READY |
| A4 | The signal table has **no connection to the hero copy beside it** — the credit-quality/visibility claim on the left and the table on the right read as two unrelated elements. Tie them together so the table visibly illustrates the claim. Same defect as H5 on the homepage. | A | READY |
| A5 | "The exposure" section: rewrite the H2, which currently fails to convey that there is **no balance-sheet exposure**. **DECIDED (Q7):** fix the headline and the three cards (A7–A9) in place; do **not** repurpose the section into "why we need your ERP data". That argument goes in "What you get / your obligations", where A12 already makes ERP access the centrepiece. | O | READY |
| A6 | Ales flagged one paragraph in "The exposure" as worth moving up near the hero/table, but didn't identify which. **DECIDED (Q8): skip for now**, implement Oscar's A5 change instead, and raise it with Ales afterwards. A4 already fixes the copy/table disconnect this was probably aimed at. | A | DEFERRED |
| A7 | Card "You can't map what you don't buy from" is **factually wrong**. Anchors *do* buy from the deeper tiers, just not directly: whatever the deep tier does is priced into the tier 1 invoice. Replace with: **you have no direct commercial relationship, so you have no line of sight**. | O | READY |
| A8 | Card "Financial stress precedes operational failure" is correct but not framed for the anchor. Spell out how the anchor *feels* it: manufacturing stalls, goods not delivered to the end customer, delays. | O | READY |
| A9 | Card "Programs can't reach far enough to help" — wrong message. What we want to say: there is now a way for their tier 2+ suppliers to access financing **at better terms, without building out a full credit line**. | O | READY |
| A10 | "What you get": right content, too much of it. Cut from five items to **three**, larger text, on the left. | O | READY |
| A11 | Of those five, **"Resilience, not just insight" must survive the cut** and move earlier in the list. Ales: as written, visibility is the only benefit that reads clearly to an anchor; supply-chain **flexibility and resilience** needs to be stated explicitly — financing the suppliers is what keeps the chain operating. | A | READY |
| A12 | "Your obligations": **ERP access is the important one** — keep it. The "what you never take on" list underneath is repetitive; cut it. | O | READY |
| A13 | "Participation — four steps, and none of them touch treasury". **DECIDED (Q9): the compromise.** Keep a visible sequence, because Ales valued it as a mechanics explanation, but restructure it so ownership is unmistakable: **split the steps into "your part" (one step: grant ERP data access) and "our part" (we build the chain, verify each transaction, fund it, and feed intelligence back)**. Delete "Pick one programme" outright; it misrepresents the product. Reframe the whole block away from programme-enrolment and toward **per-invoice financing, repeated for every invoice a tier 2+ wants funded**. Retitle: "and none of them touch treasury" survives only if "four steps" doesn't. | A + O | READY |
| A14 | Final CTA: delete "programme" language (G3) and reduce to **a single CTA: "OEM / Anchor — talk to us."** | O | READY |
| A15 | Broad simplification pass. Ales clicked through anchors and tier 1 and called the overall structure and detail level **"very complicated"**, without line-item detail. Treat as a mandate to apply G2, G7 and G8 aggressively across both pages. | A | READY |

---

## 4. `tier-1.html` (Tier 1)

Oscar gives the only line-item feedback here. Ales gave no specifics but did include this page in his "very complicated" complexity flag (A15), which corroborates T1-2. He also thinks a **Part 4 covering tier 1 may exist** (see Q13).

| ID | Change | Source | Status |
|---|---|---|---|
| T1-1 | Remove the `For tier 1 suppliers` pill. | O | READY |
| T1-2 | **This should be the shortest, simplest page on the site.** Tier 1 will be pushed into this by both their tier 2+ suppliers and the anchor. Target: scannable in 2–3 minutes. | O, corroborated by A | READY |
| T1-3 | The only thing we need from tier 1 is **ERP access**, so we can validate both halves of the chain: anchor → tier 1, and tier 1 → tier 2+. Make that the spine of the page. | O | READY |
| T1-4 | Their benefit is **comfort**: their suppliers get financed without tier 1 setting up a programme or laying out its own cash. | O | READY |
| T1-5 | Strip information already covered on the Overview and Anchor pages. A curious tier 1 can read the anchor page. | O | READY |
| T1-6 | CTA: get in touch with us, **or forward this to your anchor** so they can activate the right person. | O | READY |

---

## 5. `tier-2.html` (Tier 2+)

Ales' overall read: this is currently the most appealing and complete page on the site.

| ID | Change | Source | Status |
|---|---|---|---|
| T2-1 | Remove the `For tier 2 suppliers and beyond` pill. | O | READY |
| T2-2 | Hero H1 "You won the order. You shouldn't have to fund it yourself." **DECIDED (Q11): Oscar's angle wins.** Drop the unfairness framing; they *should* be able to fund their own order, and claiming otherwise is inaccurate. New message: **you can access better rates, because we build the evidenced relationship with the anchor/OEM the goods are ultimately delivered to.** Ales' provocative variant is retained as the documented A/B test alternative (G10), not built. | O over A | READY (copy pass, B3) |
| T2-3 | Page-wide positioning: **quick, easy access to capital at better rates**. Per Q11, "fairness" is demoted from a primary value prop; keep speed and ease, drop the injustice framing. | A, revised by Q11 | READY |
| T2-4 | Shorten the hero body copy. **Keep** the 60–120 day payment-terms point; it lands. Just make it tighter. | O | READY |
| T2-5 | Hero CTA "Apply for a transaction" is good; no change. | O | No action |
| T2-6 | Hero-right "Funding application" panel (invoice #, PO matching, delivery ack, "story complete") is too technical and process-led for this audience. **DECIDED (Q12): option (c)** — show **how we build the anchor relationship** even without a direct commercial contract, so tier 2 sees that the anchor and tier 1 are participating and want them funded. This is what justifies the better-rates headline from Q11. Option (b), "what we need from you", is already covered by "Your side of the application" lower down the page. | BOTH | READY |
| T2-7 | "Where you are today — Two bad options and no third one". **DECIDED (Q13): Oscar's.** Rename to **"Your current options"** (fund it yourself / borrow commercially) and cut each box to **≤10 words**; they already know what these mean, so explaining them adds nothing. Ales had no objection to the section, so trimming it costs nothing. | O over A | READY |
| T2-8 | The `×` list under "What neither option recognises" ("Your rating, not the chain's…", collateral, guarantees). | A: consider removing or trimming; it over-explains the anchor link instead of addressing what tier 2 actually needs. O: the content is correct, just make it concise. | READY (converge on: keep, cut hard) |
| T2-9 | "What you get" section: the current H2 frames it as *financing not on your balance sheet*. For tier 2 that's irrelevant — they're not lending, so working capital isn't the issue. Reframe to: **the solution gives them fast working capital**, which matters most when a PO arrives bigger than they forecast or planned for; that oversized PO is what breaks the chain. | O | READY |
| T2-10 | Reduce the 6 benefits to **3 strong ones** rather than 6 weak ones. | BOTH | READY |
| T2-11 | **Factual fix:** "Cash at delivery" is wrong. It's **cash when the invoice is accepted by tier 1.** | O | READY |
| T2-12 | "Better terms than your high street bank": say it better — what we actually do is **connect them to the anchor's credit rating**. | O | READY |
| T2-13 | "No programme to join": correct, keep. (This is the sanctioned use of "programme" per G3.) | O | READY |
| T2-14 | "Take the next order" → reframe as **increased planning capacity / financial stability**. | O | READY |
| T2-15 | "No personal guarantees on the chain": correct, just shorter and clearer. | O | READY |
| T2-16 | "A decision that keeps pace with production" is fluff. Improve it or drop it (drop is fine given T2-10). | O | READY |
| T2-17 | "Your side of the application" (4 steps): **both reviewers praise this.** Keep the content. Make each step's subtitle text bigger; tighten the wording. **Colour-highlight the three documents** (invoice to tier 1, purchase order, delivery note / goods received) so it's obvious those are the three things needed to start. | BOTH | READY |
| T2-18 | **DECIDED (Q10): "Your side of the application" stays on this page.** It's the page's conversion step and a role-specific ask. What moves to How it works (G7) is the *verification internals*: how we assemble and corroborate the chain. Rule applied consistently with A13 — **"what you do" lives on the role page, "what we do" lives on How it works.** | A + O | READY |
| T2-19 | Ales' TASK-T9 confirms his flow-diagram decision applies to **role pages as well as the homepage**: the demand-cascade / invoice-return diagram exists in exactly one place, `how-it-works.html`. Resolved under Q3. | A | READY |
| T2-20 | Final CTA "Start with one invoice": good, keep. Just shorten the sub-headline copy. | BOTH | READY |

---

## 6. `how-it-works.html`

Oscar only; Ales' notes never reach this page. Note that Q3 and Q10 both push content *onto* it (the cascade diagram, and the verification internals displaced from the role pages), so it ends up carrying more than either reviewer actually saw. See B5.

| ID | Change | Status |
|---|---|---|
| W1 | Remove the `The mechanics` pill. | READY |
| W2 | Hero H1 "A story a funder can underwrite" — replace per G4 (hero position). The two step-title uses of "story" further down this page **stay** (see §1.1). | READY |
| W3 | Cut the hero sub-paragraph to roughly 10 words. Oscar's own draft: *"This is not a programme. We take data from the supply chain to verify relationships and deliver funding."* | READY |
| W4 | "The chain" section: the H2 is clear and concise, keep it. | No action |
| W5 | In the same section, relabel the blocks **step A/B/C → step 1/2/3**, improve the spacing, and summarise the body text under each. The sequence is correct: (1) PO/contract in the ERP from anchor to tier 1; (2) PO from tier 1 to tier 2; (3) after production, a financeable invoice from tier 2 to tier 1. **Per Q3 this is now the site's only cascade diagram**, so it also inherits Oscar's two homepage fixes: one-line descriptions per node, and more breathing room between the role chip and the node title. | READY |
| W6 | "Why the link matters" should be promoted into a proper hero-style block with a summary of the data. The argument to make: funders have no access to operational data, so they can't lend against an operation at the anchor's credit quality because they can't see the anchor asking for that production. The link exists to build a **trusted, reliable information source** so the bank has certainty the operation originates from a well-rated company. | READY |
| W7 | Delete the "Access" and "And what closes the loop" boxes. Not important enough to keep. | READY |
| W8 | "End to end / following one transaction" (7 steps) is good but long. Summarise, make concise. | READY |
| W9 | "The exchange — data for liquidity" (gives/gets per role): **rebuild entirely.** Already covered on the role pages. Replace with a bare two-column table: left = Anchor / Tier 1 / Tier 2+, right = the benefit in ~5 words. | READY |
| W10 | "Compared with conventional SCF": good concept, bad execution. Redo as a **feature comparison table with green ticks and red crosses** marking where we differ, with minimal text. | READY |
| W11 | **Rebuild the FAQ.** Current questions feel weak. No item-by-item feedback given — build better ones from the feedback in this document. Must respect G11: no AI claims. | DECIDE (Q15 — draft the question set for review first) |

---

## 7. Decisions — RESOLVED 2026-08-06

All 13 open questions are now closed except Q15, which only asks whether to review the FAQ draft first.

| # | Decision | Rationale |
|---|---|---|
| Q1 | Em/en dashes go; **hyphens in compound words stay**. Wordmark is **deeptier**, one word, used for the product/solution. | — |
| Q2 | **Mixed by position:** "story" out of heroes and section headlines, retained in body copy and step titles. Formal term in headlines: "verified transaction record". | Honours Oscar at the points of highest visibility while keeping the framing Ales liked. Per-instance audit in §1.1. |
| Q3 | Cascade diagram **removed from homepage and role pages**; lives only on How it works. | Ales stated it twice as a firm decision and ranked it #1. |
| Q4 | "Three positions in the chain" **moves above** the solution section. | Follows from Q3. |
| Q5 | Homepage 4-item strip **consolidated into one line inside the hero**. | Kills the disconnect Ales flagged and the low-information labels Oscar flagged. |
| Q6 | "The gap in one sentence" **kept, split into two short sentences**. | Preserves what Oscar praised, fixes the density Ales flagged. |
| Q7 | Anchor "The exposure": **fix headline and cards in place**; ERP-data argument goes in "What you get". | Avoids saying the same thing twice on one page. |
| Q8 | A6 **deferred**; implement Oscar's A5 instead and raise with Ales later. | Ales' note is unimplementable as transcribed. |
| Q9 | Anchor "Participation": **the compromise** — keep the sequence, split it into "your part" (grant ERP access) vs "our part", delete "Pick one programme". | Ales valued the mechanics explanation; Oscar's objection was product accuracy, not style. Both are satisfiable. |
| Q10 | **Both step-by-step blocks stay on their role pages.** Rule: "what you do" on the role page, "what we do" on How it works. | Single consistent answer, as Ales asked. |
| Q11 | Tier 2+ hero: **Oscar's better-rates angle.** Ales' unfairness variant documented as the A/B alternative. | The accurate claim, and it's the actual product. |
| Q12 | Tier 2+ hero panel: **option (c)**, how we build the anchor relationship. | Justifies the Q11 headline; (b) duplicates content lower on the page. |
| Q13 | Tier 2+ "Two bad options": **Oscar's** rename and hard cut. | Trimming a section Ales already liked costs nothing. |
| Q14 | Tier 1 is last in the build order; no answer needed yet. See §7.1. | — |

**New constraint added from this round:** G11 — no AI claims anywhere.

### 7.1 Q14, explained

Ales' feedback came from a set of Loom screen recordings; his notes label them **Part 1** (homepage), **Part 2** (tier 2+), and **Part 3** (anchor page, plus the flow-diagram decision). At the end of Part 3 he clicks through to the **tier 1** page, says the structure feels "very complicated" and that he needs more time with it — and then stops. No line-item feedback for tier 1 ever arrives.

**RESOLVED: there is no Part 4.** He was thinking aloud, saying he'd need more time to organise his thoughts before giving further feedback. So Ales' input on tier 1 is limited to the "very complicated" signal (A15), and nothing further is coming.

Consequence: `tier-1.html` is built from Oscar's feedback plus A15. Both point the same way — make it much shorter — so this is not a conflict, just thinner input. No need to wait before step 6.

---

## 8. Open items and things to watch

Nothing here blocks implementation. Ordered by when it becomes relevant.

| # | Item | Status |
|---|---|---|
| B1 | **Copy needing a written pass and sign-off**, not a mechanical edit: homepage H1 (H1), tier 2+ H1 (T2-2, per Q11), the homepage CTA line (H21, where Oscar praised the hook but "story" has to go), and the solution H2 (H11). I'll draft these and show you before they land. | Step 2 of §9 |
| B2 | **FAQ question set** (W11) to be drafted for review before it's written into the page. | Q15 |
| B3 | **A6 deferred** pending a word with Ales about which "exposure" paragraph he meant. Not on the critical path. | Raise with Ales |
| B4 | **Ales' unfairness headline** for tier 2+ is preserved as the A/B variant (G10), not built. Someone should own the test. | Research, not build |
| B5 | `how-it-works.html` is **Oscar-only** and Q10 plus G7 push more mechanics onto it, so it ends up carrying more weight than either reviewer actually saw. Worth showing Ales once rewritten. | After step 5 |
| B6 | `tier-1.html` has **no line-item input from Ales** and none is coming (no Part 4 exists; see §7.1). Built from Oscar plus A15. | Closed |

---

## 9. Suggested execution order

Ales supplied his own priority list; it's compatible with the order below, so this merges the two.

1. **Global mechanical pass** (G1, G3, G5, G6) — low risk, touches every file, do it first and in one commit.
2. **Copy pass** — draft and sign off the four headline rewrites in B1. Everything downstream inherits this vocabulary.
3. **`index.html`** — the page both reviewers covered most, and it sets the vocabulary the rest inherits. Ales' top two priorities live here (Q3 diagram removal, Q4 reordering).
4. **`tier-2.html`** — highest-value page, most detailed feedback, best understood by both reviewers.
5. **`how-it-works.html`** — absorbs the cascade diagram (Q3) and the verification mechanics displaced from the role pages (G7), so it must follow them.
6. **`anchors.html`** then **`tier-1.html`** — the two pages Ales called "very complicated" (A15). Tier 1 largely becomes a cut-down of the anchor page. Resolve Q14 before starting tier 1.
7. **New design work** — A3/A4 signal-table refinement, W10 comparison table, W11 FAQ.

---

## 10. Implementation log

### Done and verified in the browser (2026-08-06)

**`index.html` — complete.** All of G1, G1b, G4, G5, G6, G11 applied. H1–H23 done, including the two
structural changes: the cascade diagram is gone (Q3) and "Three positions in the chain" now sits at 02,
above the solution at 03 (Q4). The 4-item trust strip became one line in the hero (Q5); the hero diagram
lost its PO/invoice numbers, edge labels and "verified story" footer (H4); the three problem cards are
bullets (H8); "the gap" is two sentences (Q6); the `×` list is a bordered "The issues" panel (H10);
"Verification, not self-declaration" is promoted to a full-width spotlight and the two weaker solution
cards are gone (H14, H15).

**`tier-2.html` — complete.** T2-1 through T2-20 done. Hero rebuilt on Oscar's better-rates angle (Q11);
the technical funding-application panel is replaced by the upward relationship chain, option (c) (Q12);
"Two bad options" renamed to "Your current options" and cut to one line per card (Q13); benefits cut 6 → 3
with the factual fix on cash timing (T2-11) and the anchor-rating framing (T2-12); "Your side of the
application" kept with larger step titles and the three required documents highlighted in copper (T2-17).

Verified at 1280px and 375px: no horizontal overflow, cards equal height, spotlight collapses to one
column on mobile. Checked mechanically: zero em/en dashes, zero pills, zero `logo tbd`, wordmark is
`deeptier` everywhere, and the only surviving "story" is the tier 2+ step title that §1.1 permits. Every
remaining use of "programme" is either the "no programme" differentiator or a reference to the legacy
alternative.

New CSS: `.heronote`, `.spotlight`, `.tierstack__cap`, `.card__bullets`, `.doc--key`.

**`how-it-works.html` — complete.** W1–W11 done. Pill removed; hero now reads "One record a funder can
underwrite" and the sub-paragraph is Oscar's own one-liner (W2, W3). Chain steps relabelled 1/2/3 with
one-line descriptions and the chip-to-title gap widened from 14px to 22px, which also absorbs Oscar's two
homepage fixes for this diagram (W5, per Q3). "Why the link matters" is promoted to a full-width spotlight
carrying the funders-have-no-operational-data argument (W6); "And what closes the loop" is deleted (W7).
The seven end-to-end steps are cut to one or two short sentences each (W8). "The exchange" is now a bare
two-column table, role against benefit in about five words (W9). The comparison table is rebuilt as green
ticks and red crosses with no prose (W10) — the deeptier column is the only all-tick column, which is the
whole point. FAQ rebuilt to nine questions (W11), each answer leading with the direct answer.

Verified: zero em/en dashes, zero pills, no AI claims (G11). All six uses of "programme" are the legacy
category or the "no programme" differentiator. The one surviving "story" is the step title §1.1 permits.
At 375px the page itself does not scroll sideways; the wide comparison table scrolls inside its own
container.

New CSS: `.mark` / `.mark--yes` / `.mark--no`, `table.cmp--marks`, `table.cmp--pairs`. Removed the dead
`.brand__tbd` rule.

**`anchors.html` — complete.** A1–A15 done. Hero rewritten to "You set the chain in motion / Now see the
risk building inside it" (A2). The signal table is kept, as Ales valued it, but rebuilt to read as a health
dashboard: a summary strip (26 suppliers mapped, 2 need attention), shorter rows, no "programme A-4471"
labels, and the "signals are derived from…" footnote deleted (A3). It is now titled "What you'd see below
tier 1", which ties it directly to the visibility claim in the hero copy beside it (A4). The exposure
headline now makes clear the exposure is operational and that nothing here touches the anchor's balance
sheet (A5). All three cards rewritten: the factually wrong "you can't map what you don't buy from" is
replaced with the no-direct-relationship framing (A7), stress is described as the anchor experiences it
(A8), and the third card now says their deeper tiers can reach better terms without building a credit line
(A9). "What you get" cut 5 → 3 in larger type with resilience promoted to first (A10, A11). "What you never
take on" deleted as repetitive (A12). Participation rebuilt per Q9: "Pick one programme" is gone and the
sequence is split into one **Your part** step (grant data access) and three **Our part** steps. Single CTA
(A14). The page now contains zero instances of the word "programme".

**`tier-1.html` — complete.** T1-1 to T1-6 done, and this is now decisively the shortest page: **307 words,
about a 1.5 minute read**, four sections, against Oscar's 2–3 minute ceiling. Hero leads on comfort;
"All we need from you" is the spine and states both halves of the validation explicitly, anchor-to-you and
you-to-tier-2 (T1-3). The squeeze cards are one line each. CTA offers both routes: talk to us, or pass the
OEM page to your anchor (T1-6). I removed the five-row alternatives comparison table: its argument (paying
early costs cash, extending your own credit eats headroom) is already the squeeze section on the same page,
and `how-it-works.html` now carries the site's comparison table. Flag it if you want it back.

### Site-wide verification (all five pages)

- Zero dashes-as-punctuation in **every** form: literal Unicode `‒ – — ―`, named entities, numeric
  entities, and spaced hyphens. Confirmed both in source and against the browser-rendered text of all five
  pages, including `<title>` and meta description. Zero pills, zero `logo tbd`, zero `Deeptier`.
- Every one of the 15 remaining "programme" uses is a negation ("no programme", "not a programme") or a
  reference to the legacy category. None describes our solution.
- Only two "story" uses remain, both step titles that §1.1 permits.
- No AI claims anywhere (G11).
- No broken internal links or dangling `#anchor` targets; no CSS class used in markup without a definition.
- No console errors. All five pages: exactly one `h1`, a populated `<title>`, no horizontal overflow at
  1280px or 375px.
- Body copy reduced: index &minus;42%, tier 1 &minus;43%, how it works &minus;30%, tier 2+ &minus;28%,
  anchors &minus;16%.

### Needs review rather than more building

- **FAQ rebuilt a second time (W11, final).** Now 11 questions in three labelled groups: *What this is*,
  *Money and risk*, *Data and practicalities*. Four questions are new, added because the rewritten site
  raises them and then never answers them: **is this factoring / a receivables sale** (the homepage says
  "not a receivables sale" without explaining), **what does it cost and who pays**, **how much work is the
  ERP connection** (the real blocker for the one thing we ask of anchors and tier 1s), and **how quickly can
  a transaction be funded** (speed is a headline value prop everywhere else). "Who takes the credit risk"
  was widened to cover the question a supplier actually asks: what if my customer doesn't pay. "Data" and
  "who else can see it" were merged, since confidentiality is the anchor's first objection to ERP access.
  Dropped "what does the anchor learn about its suppliers", which the anchor page now covers in full.

  **Three answers state a principle where the business has not set a policy, and need real content before
  launch:** cost (no numbers given), funding speed (no turnaround committed), and recourse. On recourse the
  answer deliberately says the funder's terms decide, and separates that from the "no personal guarantees"
  claim made on the tier 2+ page, which is about guarantees and collateral rather than recourse. Worth a
  legal read.
- The four headline rewrites logged in B1 are live on `index.html` and `tier-2.html`.
