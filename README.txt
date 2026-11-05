OCTAGON HQ — Fully Static Build
================================
The complete app as pure HTML/JS/CSS. No server, no database, no build step.
Your universes live in the browser's localStorage on whatever device you
open it from. Includes the splash screen (halftone loading intro + ENTER
button, reveal follows your cursor), the Khabib recalibration (OVR 95),
and the CAREER SYSTEMS update: medical suspensions, fight readiness,
injuries, evidence-based fighter development, and the AI matchmaker
(auto-booked UFC-prime cards across every division).

This build is configured for ROOT deployment (served at "/").
If you host it under a subfolder (e.g. github.io/<repo-name>), rebuild
instead with:  node scripts/build-static.mjs --base /<repo-name>


HOW TO RUN
  Any of these works:

  1. Python (usually preinstalled):
         cd octagon-hq-static
         python3 -m http.server 8000
         open http://localhost:8000

  2. Node/Bun:
         bunx serve octagon-hq-static
         npx serve octagon-hq-static

  3. Any static host: GitHub Pages, Netlify, Vercel, nginx, Apache —
     just upload the folder contents as-is.

  4. A USB stick / shared folder: copy + serve locally anytime.

  Note: opening index.html directly via file:// is the ONE thing that does
  not work (browsers block module scripts on file://). Use a server above —
  takes one command.


GITHUB PAGES — TWO WAYS
───────────────────────
  A) Let GitHub build it (recommended):
     - Push the repo to GitHub (branch main or master).
     - Repo Settings → Pages → Source: "GitHub Actions".
     - Done. .github/workflows/deploy.yml builds and deploys on every push.
     - It auto-detects the base path: user/org sites (yourname.github.io)
       deploy at "/", project sites deploy at "/<repo-name>".
     - Requirements on the runner: none (bun is set up by the workflow).

  B) Upload this zip's folder manually:
     - User/org site (yourname.github.io repo): drop the contents of
       octagon-hq-static/ at the repo root, commit, push. Works as-is.
     - Project site (any other repo): the app must be rebuilt with the
       /<repo-name> base path — use option A, or locally run:
           node scripts/build-static.mjs --base /<repo-name>
       then upload out/ to a /docs folder or the gh-pages branch.
     - Keep the .nojekyll file! Without it, GitHub Pages runs Jekyll and
       silently deletes the _next/ folder (it starts with an underscore)
       → the site loads as a blank dark page.

  The .nojekyll file is included in this zip on purpose. Don't delete it.


WHAT'S INSIDE
  index.html          the app shell
  _next/              the app code (chunks, styles)
  splash/             the three loading-screen photos
  favicon.svg         octagon favicon (self-contained)
  .nojekyll           required for GitHub Pages (keeps _next/ alive)
  logo.svg, robots.txt, 404.html

  (api/roster-dump — the 2.1MB build-time roster JSON — is intentionally
  pruned from this zip: nothing fetches it at runtime.)


SPLASH SCREEN
  Cycles three fight photos as a halftone print — dots swell into the real
  photo under your cursor. Move the mouse to reveal, click for bursts, then
  hit ENTER THE OCTAGON (Enter key works too).


CAREER SYSTEMS (v4)
  Realism presets per universe (picked at creation):
    SANDBOX    unrestricted, frozen ratings — the classic behavior
    REALISTIC  medical suspensions + readiness + availability + living
               undercards around solo careers (no random injuries)
    FULL SIM   realistic + injuries (cuts, hand/wrist, knee/leg,
               shoulder/arm, head) with long-term setbacks
  The AI MATCHMAKER button (Events tab) replaced the old card generator:
  title-fight main events, contender wars, the Fight Night prospect
  ladder, rotating divisions, availability-aware, no rematch grind.
