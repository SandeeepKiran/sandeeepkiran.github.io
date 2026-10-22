# AGENTS.md — sandeeepkiran.github.io (site switch)

Read this first. Single source of truth for AI agents (Claude Code, Cursor, Codex) in this repo.

## What this is
- The GitHub Pages user site `https://sandeeepkiran.github.io/`. Repo: `SandeeepKiran/sandeeepkiran.github.io` (PUBLIC).
- It holds **no site code**. It is a switch. The designs live in the repo `Mousy-Portfolio`
  (local folder `Videos\Project - Mousy Portfolio`), one design per branch.
- Files: `live.txt` (one word: a Mousy-Portfolio branch), `README.md`, `.github/workflows/deploy.yml`.

## How a deploy works
1. A run starts on a push to `main`, on the hourly schedule (`17 * * * *`), or on the **Run workflow** button.
2. The workflow clones Mousy-Portfolio over public HTTPS. Why: no token is needed, so Mousy-Portfolio must stay public.
3. It downloads `.github/build-site.sh` from Mousy-Portfolio `main` and runs it with the word in `live.txt`.
4. Result: `/` = the branch in `live.txt`. `/<branch>/` = every design branch (not `main`).
5. `live.txt` matching ignores capitals. The URL paths are case-sensitive (`/MousyGenshinPreview/`).
6. No custom secret. The workflow uses only the built-in `github.token` (keep-alive step).

## Change what is live
1. Check that the branch exists: `git ls-remote --heads https://github.com/SandeeepKiran/Mousy-Portfolio.git`.
2. Replace the one word in `live.txt` with that branch name.
3. Commit and push to `main` (Claude Code only, see Rules). The push starts a deploy.
- If the word matches no branch, the build fails and the old site stays live.
- Do not confuse this `live.txt` with Mousy-Portfolio's own `live.txt`. That one controls `/Mousy-Portfolio/` only.

## Check a deploy
1. Run `gh run list -R SandeeepKiran/sandeeepkiran.github.io --limit 5`.
2. Make sure the newest run shows `completed success`.
3. In Firefox, open `https://sandeeepkiran.github.io/` and hard-refresh (Ctrl+F5).

## Where to edit the real site
- Edit designs in `Project - Mousy Portfolio`, on the design branch. Read that repo's `AGENTS.md` first.
- Edit `build-site.sh` only in Mousy-Portfolio `main`. Keep its 3 arguments stable. Why: this repo calls it.
- A push to a Mousy branch shows here on the next scheduled run, or press **Run workflow** to update now.

## Rules
- The repo is PUBLIC. Never add private info (personal notes, secrets, work material).
- Never push unless you are Claude Code with the personal account `SandeeepKiran`. Follow the `safe-push` skill.
- Never add AI co-author trailers (`Co-Authored-By: …`, "Generated with …") to commits or PRs.
- Do not delete the keep-alive step. Why: GitHub pauses schedules in quiet public repos after 60 days.
- Do not add site files here. Why: the build replaces the whole site with Mousy-Portfolio output.

## Open questions
- The schedule says hourly, but real scheduled runs come about every 3–5 hours (GitHub delays). Is that OK?
- Can a design branch named `kitsune-labs` or `Mousy-Portfolio` hide those project sites? Not tested. Avoid both names.
