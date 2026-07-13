# HMCTS API Marketplace — design mockup

A static front-end mockup of the HMCTS API Marketplace, restructured to follow the
format and layout of the [NHS Developer and integration hub](https://digital.nhs.uk/developer).

This is a design/content mockup only — there is no backend. Forms show a mock
confirmation on submit; nothing is actually sent anywhere. The 6 APIs shown in the
catalogue are illustrative placeholders based on the domains described in the
source content, not real HMCTS API data.

## View it live

Once GitHub Pages is enabled for this repo (see below), the site will be available at:

```
https://<your-org-or-username>.github.io/<repo-name>/
```

## Pages

| Page | File |
|---|---|
| Home | `index.html` |
| API Catalogue | `api-catalogue.html` |
| API detail (example) | `api-detail.html?api=crime-prosecution-case-details` |
| Onboarding guide | `onboarding-guide.html` |
| Consumer guidance | `consumer-guidance.html` |
| Producer standards | `producer-standards.html` |
| Data governance standards | `data-governance.html` |
| Request API access | `request-api.html` |
| Publish an API | `publish-api.html` |
| Request a new API | `request-new-api.html` |
| Sign in / Register | `sign-in.html` |

## Running locally

No build step — just open `index.html` in a browser, or serve the folder with any
static file server, for example:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

## Enabling GitHub Pages

1. Push this folder's contents to the root of a GitHub repository (branch `main`).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch".
4. Set **Branch** to `main` and folder to `/ (root)`.
5. Save. GitHub will publish the site at `https://<org-or-user>.github.io/<repo-name>/`
   within a minute or two.

## Structure

```
.
├── index.html
├── api-catalogue.html
├── api-detail.html
├── onboarding-guide.html
├── consumer-guidance.html
├── producer-standards.html
├── data-governance.html
├── request-api.html
├── publish-api.html
├── request-new-api.html
├── sign-in.html
└── assets/
    ├── styles.css      — shared stylesheet
    ├── scripts.js      — nav, tabs, catalogue filtering, mock form submission
    └── api-data.js     — mock dataset for the API catalogue and detail page
```

All internal links are relative, so the site works whether it's served from a
domain root or a GitHub Pages project subpath.
