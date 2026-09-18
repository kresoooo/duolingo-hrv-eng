# Task: publish Talk Shop to GitHub Pages

Repo: git@github.com:kresoooo/duolingo-hrv-eng.git (public, currently empty)
Target URL: https://kresoooo.github.io/duolingo-hrv-eng/

You are running in the folder that contains the app files, unzipped from duolingo-hrv-eng.zip:
- index.html  (the whole app, single file - do NOT edit or reformat it)
- sw.js       (service worker for offline cache)
- README.md   (deployment notes, Croatian)
- .nojekyll   (tells GitHub Pages not to run Jekyll)

If any of these files is missing, stop and say which one.

## Steps

1. Initialise the repo and push (main branch):
   git init
   git add .
   git commit -m "Talk Shop: English trainer (Duolingo-style), first version"
   git branch -M main
   git remote add origin git@github.com:kresoooo/duolingo-hrv-eng.git
   git push -u origin main

   If the push fails with "Permission denied (publickey)", switch to HTTPS and retry:
   git remote set-url origin https://github.com/kresoooo/duolingo-hrv-eng.git
   git push -u origin main
   (If git asks for a password, a GitHub Personal Access Token is needed, not the account password; `gh auth login` also sets this up.)

2. Enable GitHub Pages from the main branch, root folder. Preferred, with the GitHub CLI:
   gh api -X POST repos/kresoooo/duolingo-hrv-eng/pages -f "source[branch]=main" -f "source[path]=/"
   If that returns 409 (already exists), that is fine.
   If `gh` is not installed or not logged in (`gh auth status`), tell the user to do it in the browser instead:
   Settings -> Pages -> Build and deployment -> Source "Deploy from a branch" -> Branch main, folder "/ (root)" -> Save.

3. Wait for the deployment, then verify (retry every 20 seconds, up to 5 minutes):
   curl -s -o /dev/null -w "%{http_code}\n" https://kresoooo.github.io/duolingo-hrv-eng/
   Expected: 200. Also check that the page contains the app:
   curl -s https://kresoooo.github.io/duolingo-hrv-eng/ | grep -c "Talk Shop"
   Expected: a number greater than 0.

4. Report back with:
   - the live URL,
   - whether Pages was enabled by CLI or still needs the browser step,
   - anything that failed.

## Do not
- Do not change index.html, sw.js or their names (the service worker path and manifest depend on them).
- Do not add a build step, framework, package.json, or CI workflow. This is a static site: two files.
- Do not create a custom domain or change repo visibility.

## After this task (for the user, not for you)
On the phone: open the URL in Safari, Share -> Add to Home Screen.
In the app: Deck -> Settings -> paste the Claude API key (feedback) and a GitHub token with the `gist` scope (progress sync). Details are in README.md.
