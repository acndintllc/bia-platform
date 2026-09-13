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

## 1a. Upstream bases

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

## 2. Licensing and repository layout

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

## 3. Monorepo structure

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

## 4. Shared infrastructure

- **Supabase** — one project, five schemas
- **Stripe** — one account, three subscription products
- **Cloudflare R2** — one bucket, namespaced per app (zero egress fees)
- **Domain** — root plus a subdomain per app
- **Deployment** — each app containerized, deployed from its repository

---

## 5. Per-app plan

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

## 6. Operations

**CI/CD** — GitHub Actions, one workflow per app, triggered by changes
under that app's path.

**Monitoring** — error tracking, performance monitoring, billing webhooks.

---

## 7. Build order

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

## 8. Decisions locked

- Five apps
- Bundled subscription tiers
- All TypeScript, monorepo plus shared core
- AGPL-3.0 throughout
- Misskey forks kept in separate repositories, HTTP-only coupling
- One Supabase project, five schemas
- Cloudflare R2 for storage
