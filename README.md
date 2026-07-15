# HMCTS API Marketplace — design mockup

A front-end mockup of the HMCTS API Marketplace, originally structured to follow the
format and layout of the [NHS Developer and integration hub](https://digital.nhs.uk/developer),
then rebuilt with HMCTS's own brand guidelines (colours, logo, typography) and
its own distinct layout.

Most of the site is a static content mockup — forms like "Request API access"
or "Publish an API" show a mock confirmation on submit; nothing is actually
sent anywhere. **Sign in and account creation are the exception**: these are
wired up to a real backend (see [Authentication](#authentication) below), so
accounts, logins and sessions are genuinely functional, not mocked.

The APIs shown in the catalogue and elsewhere are illustrative placeholders
based on the domains described in the original source content, not real
HMCTS API data.

## View it live

```
https://zaheeriqbal-hmcts.github.io/api-marketplace/
```

(Or, if hosted elsewhere: `https://<your-org-or-username>.github.io/<repo-name>/`)

## Pages

| Page | File |
|---|---|
| Home | `index.html` |
| API Catalogue | `api-catalogue.html` |
| API detail (example) | `api-detail.html?api=crime-prosecution-case-details` |
| Onboarding guide | `onboarding-guide.html` |
| Getting started | `getting-started.html` |
| Consumer guidance | `consumer-guidance.html` |
| Producer standards | `producer-standards.html` |
| Data governance standards | `data-governance.html` |
| Documentation, guides and tutorials | `documentation.html` |
| A to Z of developer resources | `resources-a-z.html` |
| Glossary of developer terms | `glossary.html` |
| API platform case studies | `case-studies.html` |
| Building justice sector software | `building-software.html` |
| Introduction to justice sector technology | `technology-introduction.html` |
| Our API technologies | `our-api-technologies.html` |
| HMCTS architecture | `architecture.html` |
| HMCTS architecture principles | `architecture-principles.html` |
| Our capabilities | `our-capabilities.html` |
| Developer community | `community.html` |
| Help and support | `help-and-support.html` |
| Request API access | `request-api.html` |
| Publish an API | `publish-api.html` |
| Request a new API | `request-new-api.html` |
| Contact the marketplace team | `contact.html` |
| **Sign in** (real auth) | `sign-in.html` |
| **Create an account** (real auth) | `register.html` |
| **My developer account** (requires sign-in) | `account.html` |
| **My applications and teams** (app registration wizard) | `my-applications.html` |

## Authentication

Sign in and account creation are wired up to a real backend, kept in a
separate repository: [`hmcts-api-marketplace-auth`](https://github.com/ZaheerIqbal-HMCTS/hmcts-api-marketplace-auth),
deployed on [Render](https://render.com) at
`https://hmcts-api-marketplace-auth.onrender.com`.

- Accounts are stored in a real Postgres database (not a file on the app's
  own disk), so they persist across redeploys
- Passwords are hashed with bcrypt — never stored in plain text
- Sessions use an `httpOnly` JWT cookie, not readable by page JavaScript
- Every regular page checks your sign-in status on load and updates the
  header nav accordingly ("Sign in" vs "My account (Name)" + "Sign out")

See that repo's own README for how to run or redeploy the backend, add
environment variables, or set up the database.

**Known limitation:** Render's free tier spins down after 15 minutes of
inactivity. The first request after a quiet period can take 30-60 seconds to
respond (including the header's sign-in check on any page) — this is
expected free-tier behaviour, not a bug.

## Running locally

No build step for the static pages — just open `index.html` in a browser, or
serve the folder with any static file server, for example:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

Sign-in/account pages will still talk to the live Render backend even when
run locally, unless you point `API_BASE` (near the top of the `<script>`
block in `sign-in.html`, `register.html`, `account.html`, and
`assets/scripts.js`) at a locally-running copy of the auth server instead.

## Enabling GitHub Pages

1. Push this folder's contents to the root of a GitHub repository (branch `main`).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch".
4. Set **Branch** to `main` and folder to `/ (root)`.
5. Save. GitHub will publish the site at `https://<org-or-user>.github.io/<repo-name>/`
   within a minute or two.

## Brand guidelines

The site follows HMCTS's real brand guidelines (provided separately, not
included in this repo):

- **Colours**: HMCTS blue (`#0096d6`), HMCTS navy (`#002d59`), black, with
  Purple, Golden, Grass green, Teal, Orange and Rose red used as secondary/
  accent colours. Text is navy or black; white text is only used where
  contrast has been checked (e.g. large dark hero sections), not as a
  default.
- **Typography**: Arial as the primary typeface throughout, per the brand
  guide's "almost always use Arial" rule.
- **Logo**: the real HMCTS crest + wordmark (`assets/hmcts-logo-black.png`),
  used unmodified — no filters, no recolouring, no boxing — only ever placed
  on backgrounds with sufficient contrast (light backgrounds, since only the
  black version of the logo is available). Where a page has a dark hero
  (e.g. `sign-in.html`), the logo sits in its own separate white bar rather
  than being altered to fit the dark background.

## Structure

```
.
├── index.html, api-catalogue.html, api-detail.html
├── onboarding-guide.html, getting-started.html, consumer-guidance.html
├── producer-standards.html, data-governance.html
├── documentation.html, resources-a-z.html, glossary.html, case-studies.html
├── building-software.html, technology-introduction.html, our-api-technologies.html
├── architecture.html, architecture-principles.html, our-capabilities.html
├── community.html, help-and-support.html, contact.html
├── request-api.html, publish-api.html, request-new-api.html
├── sign-in.html, register.html, account.html, my-applications.html
└── assets/
    ├── styles.css           — shared stylesheet (design tokens, all page styles)
    ├── scripts.js           — nav, tabs, catalogue filtering, mock form
    │                          submission, and the site-wide sign-in status check
    ├── api-data.js          — mock dataset for the API catalogue and detail page
    └── hmcts-logo-black.png — real HMCTS logo (black version)
```

All internal links are relative, so the site works whether it's served from a
domain root or a GitHub Pages project subpath.
