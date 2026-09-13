# BIA Platform — Foundation Architecture

**Status:** Locked, ready for implementation
**Maintainer:** ACND INT. LLC.
**License:** AGPL-3.0

BIA — the Black Internet Alliance — is five applications on one shared
platform layer. Members get a single account, a single subscription and a
federated identity across all of them.

---

## 1. The portfolio


| App | Type | Base | Stack |
|---|---|---|---|
| **BlackGPT** | AI assistant | Own codebase | Next.js + Qwen |
| **Blackbook** | Text social | Misskey | TypeScript |
| **Blackgram** | AI image gallery | Misskey | TypeScript |
| **Blackflix** | AI film platform | Strapi (Community Edition) | TypeScript |
| **Blackboard** | Services network | OpenCollective (api + frontend) | TypeScript |

All TypeScript. All built on proven bases that already solve their hard
problem — federation, streaming, identity, payments.

---

## 2. Upstream bases


Three external projects cover all five applications. Misskey serves two.

| Base | Branch | Covers | License |
|---|---|---|---|
| `misskey-dev/misskey` | `develop` | Blackbook, Blackgram | AGPL-3.0 |
| `strapi/strapi` | `develop` | Blackflix | MIT, except `ee/` |
| `opencollective/opencollective-api` | `main` | Blackboard (backend) | MIT |
| `opencollective/opencollective-frontend` | `main` | Blackboard (UI) | MIT |

**OpenCollective is two repositories.** `opencollective-api` is a GraphQL
backend with no interface; Blackboard needs `opencollective-frontend`
(React/Next.js) as well. Both MIT, but it is twice the integration work a
single repository would imply.

**Strapi is MIT except under `ee/`.** Anything in an `ee/` directory is
Enterprise Edition and falls under a commercial license, not MIT. Holding
an account on Strapi's cloud offering has the same effect.

> **Rule for Blackflix:** never modify, copy or depend on code under an
> `ee/` directory. Community Edition only.

---

## 3. Licensing and repository layout


Everything is AGPL-3.0. Fork it, remix it, run it — but a modified version
offered over a network must publish its modifications. The platform was
built on free software and returns on the same terms.

Blackbook and Blackgram derive from Misskey, which is AGPL-3.0, so their
license is inherited rather than chosen. The remaining code is AGPL-3.0 by
decision.

| Repository | Contents | Visibility |
|---|---|---|
| `bia-platform` | core, gpt, flix, board | Public |
| `blackbook` | Misskey fork | Public |
| `blackgram` | Misskey fork | Public |

**One rule keeps the boundary clean:** the Misskey forks never import BIA
core. They talk to it over HTTP. Arm's-length API calls between separate
programs do not create a derivative work; import statements are a far
harder argument to make. This keeps each codebase's license question
self-contained.

---

## 4. Monorepo structure


```
bia-platform/
├── core/
│   ├── auth/          Supabase client + session
│   ├── billing/       Stripe subscriptions
│   ├── identity/      ID + face verification (Stripe Identity)
│   ├── storage/       Cloudflare R2 wrapper
│   ├── api/           Shared endpoints, including for the Misskey forks
│   └── schema/        Supabase migrations
├── apps/
│   ├── gpt/           BlackGPT
│   ├── flix/          Strapi — submissions + video
│   └── board/         OpenCollective — services network
├── packages/
│   ├── shared-types/
│   └── shared-ui/
├── infra/
│   ├── docker/
│   ├── deploy/
│   └── .env.example
└── turbo.json
```

Blackbook and Blackgram live in their own repositories and consume
`core/api` over HTTP.

---

## 5. Shared infrastructure


- **Supabase** — one project, five schemas
- **Stripe** — one account, three subscription products
- **Cloudflare R2** — one bucket, namespaced per app (zero egress fees)
- **Domain** — root plus a subdomain per app
- **Deployment** — each app containerized, deployed from its repository

---

## 6. Per-app plan


### BlackGPT
Migrate to `apps/gpt/`. Wire BIA auth and billing. Apply BIA branding.
Personality wrapper and curated sources are parked for a later phase.

### Blackbook — Misskey instance
Fork Misskey. Sync users from BIA auth over the core API. Federate with
Blackgram via ActivityPub. AI moderation with a PhotoDNA hard rail.
Deployed as its own service.

### Blackgram — Misskey instance, AI-only
Same base as Blackbook, federated with it. Enforces AI-generated uploads
only — no real photographs. Images in R2.

### Blackflix — Strapi + submission layer
Schema for submissions, creators, films and festivals. Submission intake,
admin accept/reject workflow, video via a streaming CDN.

Policy:
- Eligible if accepted to compete at a recognized festival
- Membership plus upload fee required
- 100% AI-generated content
- Automated check failure → 7-day free resubmit window
- Human denial → final, no resubmit
- Days 8–30 → 50% discount, same film, one retry
- Day 31+ → full price or new submission

### Blackboard — OpenCollective + services network
Profiles become service listings with verification status.

Policy:
- ID and face verification at signup
- Verified badge means identity confirmed and face matched
- Credentials are not retained after verification
- No personal information disclosed unless the member opts in
- The platform is not responsible for transaction outcomes
- Posts moderated for violations like any other platform

---

## 7. Launch sequence


BIA is sold as one platform with entry levels. No application is released
separately.

| Phase | Tier available | Contents |
|---|---|---|
| **Launch** | Base only | Blackbook, Blackgram, Blackboard. Premium marked "coming soon". |
| **+3-6 months** | Premium | Base + BlackGPT |
| **~12 months** | Premium+ | Premium + Blackflix |

**Three of the four launch applications are containers.** Blackbook,
Blackgram and Blackboard open empty and fill from members. Empty is the
correct day-one state for a user-generated platform; the question is
whether someone can post, not whether anyone has.

**BlackGPT is not a container.** No member can fill it. It needs a corpus
the operator supplies, which is why it waits rather than shipping thin.

**Blackflix is curated, not open.** Every film passes review regardless of
how it arrives. It is not a destination for every AI-generated entry.

### The festival

A film festival sponsored by Blackflix runs ahead of its launch. It does
three jobs, in order of importance:

1. **Awareness.** Everyone who enters learns the platform exists, whether
   they ever upload or not.
2. **Qualification.** Ranking identifies who is worth reviewing first. It
   does not bypass review.
3. **Recruitment.** The top finalists are working creators. Comping them
   is signing talent, not awarding a discount.

Placement earns first rights and access at varying cost. Entrants outside
the top tiers may still pay to submit for review. The review gate never
lifts.

The metric is **entries, not uploads.** The festival is a marketing
investment that produces a qualified pipeline. Judging it by upload
conversion measures the wrong thing.

### Consequences

**Cost.** The 10,000-member projection assumed every application live,
with video roughly 80% of it. A Base-only launch is two small instances,
object storage and a database — a fraction of that. Revenue arrives a year
before the expensive application switches on, and funds it.

**Build order.** The festival precedes Blackflix, so festival
infrastructure is needed first. Blackflix splits: submission and review
are required for the festival; streaming and catalogue are required for
launch a year later.

**Billing.** Placement-based fee waivers and discounts are Stripe promotion
logic living in core, needed at festival time rather than Blackflix time.

---

## 8. BlackGPT is deferred


BlackGPT does not ship in the first release. It waits until its retrieval
layer exists.

**Why.** Every other application inherits a working product — Misskey
federates, Strapi manages content, OpenCollective handles money. BlackGPT
is the only one where the work *is* the product. Without a curated corpus
it is a chat interface over a general model, which is both undifferentiated
and a promise the platform cannot keep: general web ranking reflects who
has search budget and institutional authority, which is the bias the
platform exists to route around.

**What it needs first.** A three-tier retrieval layer:

1. **Owned corpus** — documents ingested and indexed directly. Public
   domain archives, open-access scholarship, government data, community
   contributions. This is the part nobody can reach through an API, and
   therefore the only durable advantage.
2. **Curated live sources** — a domain allowlist queried directly rather
   than through general ranking. The list is editorial policy.
3. **General fallback** — used only when the first two return nothing, and
   labelled as such.

Answers state which tier they came from. That transparency is the feature.

**Known obstacles.** Much twentieth-century Black press sits behind
exclusive digitisation agreements; pre-1929 material is public domain and
clean, the richest later period is not. Curation is ongoing labour rather
than a build, which is exactly why it is defensible. Coverage gaps are
certain, so the fallback must be honest rather than improvising.

**Consequence for pricing.** The tier model places BlackGPT alone in
Premium. With it deferred, Premium has no contents at launch. The launch
tiers need revisiting before release.

---

## 9. Operations


**CI/CD** — GitHub Actions, one workflow per app, triggered by changes
under that app's path.

**Monitoring** — error tracking, performance monitoring, billing webhooks.

---

## 10. Build order


1. Create the repositories
2. Build BIA core — auth, billing, identity, storage
3. Integrate the apps
4. Provision Supabase, one project, five schemas
5. Provision Stripe, three products
6. Register the domain and subdomains
7. Containerize
8. Deploy to staging — verify federation, shared auth, billing
9. Soft launch, then public

---

## 11. Decisions locked


- Five apps
- Bundled subscription tiers
- All TypeScript, monorepo plus shared core
- AGPL-3.0 throughout
- Misskey forks kept in separate repositories, HTTP-only coupling
- One Supabase project, five schemas
- Cloudflare R2 for storage
- BlackGPT deferred until its retrieval layer exists; core therefore needs
  no usage metering or inference budgeting in the first release

