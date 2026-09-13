# Film festival — full scope

Sponsored by Blackflix. Runs ahead of Blackflix's launch.

This is a requirements map, not a plan. It exists to make the unknowns
visible before anything is committed. Nothing here is decided.

---

## What the festival is for

1. **Awareness** — every entrant learns the platform exists
2. **Qualification** — ranking identifies who is worth reviewing first
3. **Recruitment** — finalists are working creators worth signing

Success metric is **entries**, not uploads.

---

## The obvious parts

Collecting, screening, advertising, promoting, hosting, judging, winners,
prizes, fees. Real work, but known work. The rest of this document is the
part that tends to surprise people.

---

## 1. Legal and rights — the highest-risk area

**Screening rights.** Accepting a film is not permission to show it. The
submission agreement must grant the right to screen, and to use stills and
clips in promotion. Without it, publishing a winner's film is infringement.

**Music clearance.** The most common festival trap. Filmmakers routinely
score with music they have not licensed. If the festival screens it, the
festival has exposure alongside the filmmaker. Requires an explicit
warranty from the submitter that all music is cleared or original.

**Chain of title.** Does the entrant actually own what they submitted? A
warranty and indemnity clause is standard and necessary.

**Likeness and deepfakes.** *Specific to an AI festival and significant.*
A submission using a real person's face or voice without consent is a
legal problem that lands on the festival too. Needs an explicit rule, a
submitter warranty, and a screening check. Several jurisdictions now
legislate on this directly.

**AI provenance and disclosure.** Which tools were used. Whether any
training data is disputed. Whether the work is genuinely the entrant's.
The festival's own rule is that content is AI-generated — so how that is
verified, and what disqualifies, must be defined in advance rather than
argued afterwards.

**Content classification.** Who decides what is too explicit, too violent,
or hateful? A published standard, applied by a named person, decided
before entries open.

---

## 2. Entry mechanics

- **Fee structure.** Early bird, regular and late deadlines are standard
  and materially increase revenue. Decide the ladder before opening.
- **Refunds.** What happens on withdrawal, on disqualification, on
  cancellation of the festival. Written down, or it becomes an argument.
- **Categories.** Length, genre, first-time creator, and so on. Categories
  multiply judging work — each one needs its own ranking.
- **Technical specification.** Format, codec, resolution, aspect ratio,
  maximum file size, subtitle and caption requirements. Published up front
  or the screening room becomes a support desk.
- **Where files land.** Hundreds of video files is real storage and real
  bandwidth, needed months before Blackflix exists.
- **Withdrawal.** Entrants sometimes pull films after acceptance elsewhere.

---

## 3. Judging — the largest hidden workload

**Screening volume.** 300 entries at ten minutes each is fifty hours of
viewing before any discussion. One person cannot do it. Multiple screeners
mean calibration, or scores are not comparable.

**Rubric.** Written before entries open. Without it, ranking is
indefensible and disputes have nothing to appeal to.

**Rounds.** Typically screener pass, then semifinal, then final jury. Each
round needs its own criteria and its own cut.

**Jurors.** Recruiting credible judges is its own project. They usually
expect a fee, a credit, or both. Their names are also a promotional asset,
which cuts both ways — announce them and they are committed.

**Conflicts of interest.** A juror who knows an entrant. Policy needed
before it happens, not after.

**Ties.** A tie-break rule, written down.

**Feedback.** Do entrants receive scores or notes? Generous, and a
significant support load. Decide deliberately.

---

## 4. Disputes

- **Appeals.** Is there a process, and who decides?
- **Plagiarism and provenance challenges.** Another entrant alleges a film
  is stolen or misrepresents its AI use. Needs an investigation path.
- **Post-announcement violations.** A winner is found to have breached the
  terms after prizes are public. Revocation policy, decided in advance.

---

## 5. The event itself

- Online, physical, or hybrid? Each is a different budget entirely.
- If films are screened publicly, that is a streaming event or a venue.
- Awards presentation: live, recorded, or announced in writing.
- Accessibility: captions and audio description are increasingly expected
  and in some contexts required.

---

## 6. Money

- **Revenue:** entry fees across the deadline tiers.
- **Costs:** jury fees, storage and bandwidth, promotion, platform fees,
  prize fulfilment, any venue.
- **Prize liability.** Comped years and waived upload fees are real cost
  carried on the platform's books.
- **Tax.** In the United States prizes are generally taxable income to the
  recipient, and payers may have reporting obligations. Needs confirming
  with an accountant before prizes are announced.

---

## 7. Privacy and data

- Entrant personal information: names, addresses, payment details.
- **Unreleased films are sensitive.** Entrants are trusting the festival
  with work that is not public. Storage must be access-controlled, and
  screeners must not be able to redistribute.
- Retention: how long are non-winning entries kept, and who can see them?
- Disclosure: what is published about entrants, and what stays private.

---

## 8. Distribution and discovery

**FilmFreeway is where filmmakers find festivals.** Not listing there
means being largely invisible to the intended audience. Listing means a
platform cut and a relationship the festival does not own. A new festival
also has no track record, so visibility is limited regardless.

The alternative is direct outreach, which is slower, cheaper, and builds a
relationship the platform keeps. Both can run together.

---

## 9. Timeline

Works backwards from the announcement date. A realistic cycle:

```
Rules, rubric, jury confirmed, submission platform ready   before opening
Submissions open -> early / regular / late deadlines       ~3 months
Screening rounds                                           ~6-8 weeks
Final jury                                                 ~2-3 weeks
Winners announced, prizes fulfilled
```

Roughly six months per cycle. Two cycles is about a year, which matches
Blackflix's launch horizon.

---

## 10. What has to be built

| Piece | Notes |
|---|---|
| Submission intake | Form, file upload, payment. **This is also Blackflix's upload flow** — build once. |
| Entrant accounts | Status, withdrawal, communications |
| Screening interface | Playback, scoring against the rubric, round management |
| Ranking and cuts | Aggregation, tie-breaks, category handling |
| Promotion codes | Placement-based fee waivers. **Lives in BIA core billing**, needed at festival time. |
| Notifications | Confirmation, status, acceptance, rejection, winner |
| Public site | Rules, deadlines, jury, entry, results |
| Storage | Hundreds of video files, access-controlled |

---

## Open questions

Nothing here is decided. These need answers before anything is built.

1. Online, physical or hybrid?
2. FilmFreeway, direct, or both?
3. Who judges, and are they paid?
4. What are the categories?
5. What is the entry fee ladder?
6. What exactly disqualifies an entry?
7. How is AI provenance verified?
8. Is feedback given to non-winners?
9. Who is legally running this — the LLC, or a separate entity?
10. What is the budget ceiling for cycle one?
