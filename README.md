# Metgabb Smart Elections: POC

A clickable proof of concept for a digital election campaign management and civic engagement platform. One page (`index.html`) holds four parts:

- **Admin Portal:** constituencies, candidates, volunteers, groups, tasks, campaign posts, public feedback, AI insights, reports and settings
- **Candidate Portal:** feedback from the candidate's microsite, constituency insights and an AI briefing assistant
- **Volunteer Portal:** a phone-first task list with photo and video updates
- **Public candidate microsites:** auto-generated pages where residents send feedback without logging in

Live site: https://mett-infra.github.io/Metgabb-Smart-Elections-POC/

> All people and data are fictional and only real place names are used. Social media and AI run in a clearly labelled mock mode. There is no backend, so nothing is sent anywhere.

## Demo logins

| Role | Email | Password |
|---|---|---|
| Super Admin | admin@metgabb.demo | Admin@2026 |
| Election Administrator | ops@metgabb.demo | Admin@2026 |
| Candidate (Damansara) | aisyah@metgabb.demo | Candidate@2026 |
| Candidate (Johor Bahru) | arjun@metgabb.demo | Candidate@2026 |
| Volunteer (group leader) | farid@metgabb.demo | Volunteer@2026 |
| Volunteer (group leader) | kenneth@metgabb.demo | Volunteer@2026 |

All 10 candidates use `Candidate@2026`, and all 30 volunteers use `Volunteer@2026` (email = first name @metgabb.demo). The sign-in page has one-click buttons for each role.

These are demo-only accounts. They live inside the page and protect nothing real.

## 5-minute demo script

1. **Public:** open a candidate page (e.g. Dr. Aisyah Rahman) and submit a complaint. You get a reference number back.
2. **Candidate:** sign in as `aisyah@…`. The complaint is already on the dashboard. Change its status, then ask AI Assist for a briefing note.
3. **Public:** enter the reference number under *Track* on the microsite. The new status shows up.
4. **Admin:** create a candidate. The microsite, QR code and login are generated straight away. Then create a task for *Damansara Ground Operations*.
5. **Volunteer:** sign in as `farid@…` on a phone. Open the task, attach a photo and submit an update.
6. **Admin:** open the task to see the update. *Settings → Permission tests* runs 16 access checks.

Tip: open the admin and volunteer portals in two tabs of the same browser. Updates sync between them live.

## Where the data lives

Everything is saved in the viewer's own browser (localStorage), so each person and device gets their own copy of the demo data. *Settings → System → Reset demo data* restores the original data.

## Run locally

Double-click `index.html`, or serve it:

```powershell
npx serve . -l 8080
```

Then open http://localhost:8080.

## Deploy

Every push to `main` runs `.github/workflows/deploy-pages.yml`, which publishes `index.html` (plus a copy as `404.html`) to GitHub Pages. There is no build step. One-time setup: in the repo, go to Settings → Pages → Source and choose **GitHub Actions**.

## How updates work

Each change arrives as a small `update-NNN-short-name.zip` holding only the changed files at their repo paths. The steps are:

1. Unzip it into this folder.
2. Remove any files listed for deletion.
3. Test locally.
4. Commit with the update number and push to `main`.

The site redeploys in 1 to 2 minutes.

## Path to production

Next.js + Supabase (Postgres, Auth, Storage, row-level security) on Vercel. The schema, relationships and access policies are listed in the app under *Settings → Database schema*.
