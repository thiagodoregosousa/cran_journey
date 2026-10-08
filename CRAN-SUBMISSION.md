# Submitting an R package to CRAN — the flow

A simple, reusable recipe. Two halves: **checking** (you automate) and
**submitting** (human-in-the-loop, you can't automate).

## The big picture

```
   write code
      │
      ▼
 local check  ──►  CI check (GitHub)  ──►  CRAN-platform check (email)  ──►  submit  ──►  CRAN replies (email)
 devtools::      R-CMD-check.yaml        check_win_devel()                devtools::      accept / fix & resubmit
 check()         on every push          (win-builder, ~30 min)           release()
```

Rule of thumb: **everything before "submit" is checking and can run
automatically; the submit step is deliberate and manual, by design.**

## 1. Local check (your machine, in R, from the package folder)

```r
devtools::document()   # regenerate man/ + NAMESPACE
devtools::check()      # full R CMD check  → want: 0 errors | 0 warnings | 0 notes
```

Fix everything until it is 0/0/0.

## 2. CI check (automatic, on GitHub)

On every `git push`, the **Actions** tab runs:

- **R-CMD-check** — `R CMD check` on macOS, Windows, Linux (R release/devel/oldrel).
- **pkgdown** — rebuilds the documentation website.

Just confirm both are green. A green R-CMD-check means CRAN's own checks will
almost certainly pass.

## 3. CRAN-platform check (in R, results come by email)

These upload to CRAN's build servers and **email you** the results (~30 min).
Nothing to install locally.

```r
devtools::check_win_devel()     # Windows R-devel  (CRAN's strictest)
devtools::check_win_release()   # Windows R-release
# optional, more platforms:
# rhub::rhub_check()
```

## 4. Prepare the release files

- **`DESCRIPTION`** — bump `Version` (semver: breaking changes are fine inside
  `0.x`; save `1.0.0` for a stable API). Fix `Authors@R` (roles `aut`/`cre`).
- **`NEWS.md`** — list the user-visible changes for this version; mark breaking
  changes.
- **`cran-comments.md`** — test environments + "0 errors | 0 warnings | 0 notes"
  + reverse-dependency note. (Keep it in `.Rbuildignore`.)

## 5. Submit (in R, one command)

```r
devtools::release()
```

It runs final checks, asks a few yes/no questions, builds the `.tar.gz`, and
uploads it to CRAN's submission form. (Manual alternative: upload the tarball at
<https://cran.r-project.org/submit.html>.)

## 6. Confirm + wait for CRAN (email)

- CRAN emails the **maintainer** a confirmation link → click it.
- CRAN runs their incoming checks → emails you **accept** or a list of issues.
- If issues: fix them, bump the version (e.g. `0.3` → `0.3.1`), and repeat from
  step 1.

## Where each thing lives

| Thing | Where | Who runs it |
|---|---|---|
| Local check | R console, package folder | you |
| Multi-OS check | GitHub Actions (`.github/workflows/`) | automatic on push |
| Win/R-hub check | CRAN build servers | you trigger, results by email |
| The submission | CRAN web form / `devtools::release()` | you, deliberately |
| Acceptance | CRAN servers + a human | CRAN, replies by email |

## Handy one-liners

```r
devtools::spell_check()     # catch typos CRAN will flag
urlchecker::url_check()     # verify URLs/DOIs resolve
devtools::check(remote = TRUE, manual = TRUE)  # closer to --as-cran
```
