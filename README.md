# mehedibuet11 — App Policy Site

Central hosted pages for each Android app:
- App homepage
- Privacy policy
- Terms of service

Live URL: `https://mehedibuet11.github.io`

Per-app URLs:
- App homepage: `https://mehedibuet11.github.io/apps/your-app-slug/`
- Privacy policy: `https://mehedibuet11.github.io/apps/your-app-slug/privacy/`
- Terms of service: `https://mehedibuet11.github.io/apps/your-app-slug/terms/`

## Repo structure

- `index.html`: main listing page (auto-updated)
- `app-template/`: HTML templates for the 3 pages
- `apps/<slug>/`: generated app pages
- `.github/workflows/sync.yml`: generator workflow (GitHub Actions)

## One-time setup

1) GitHub Pages
- Create a repo named exactly `mehedibuet11.github.io`
- Settings -> Pages -> Source -> set to `main` branch, `/ (root)`

2) Personal Access Token (for syncing)
- Create a classic PAT with `repo` scope
- Add repo secret in this site repo:
  - Name: `PRIVACY_SYNC_TOKEN`
  - Value: your PAT

3) OpenAI API key (for generation)
- Add repo secret in this site repo:
  - Name: `OPENAI_API_KEY`
  - Value: your OpenAI API key

Cost control rule:
- First build: generates pages when an app repo has `description.txt`
- Later builds: regenerates only when `description.txt` contains `need update` (remove it after the next sync)

## Add a new app

1) In this repo: add your app repo in `.github/workflows/sync.yml` under `APP_REPOS`.

2) In your app repo:
- Add `description.txt` at the repo root (copy from `FOR_EACH_APP_REPO/description.txt`).
- Add `.github/workflows/notify-privacy.yml` (copy from `FOR_EACH_APP_REPO/.github/workflows/notify-privacy.yml`).
- Add repo secret:
  - Name: `PRIVACY_SYNC_TOKEN`
  - Value: same PAT as the site repo

## Manual sync

If needed: GitHub -> Actions -> Sync Privacy Policies -> Run workflow

