# cran_journey

A hands-on guide to building your first R package and taking it all the way
to CRAN (the Comprehensive R Archive Network). Walks through why R packages
and reproducible research matter, how CRAN review works, and the concrete
steps from a bare folder of functions to an accepted CRAN submission.
Written for R users preparing their first package for CRAN.

## What's inside

The guide is a slide deck (`slides.pdf`, in Portuguese) with a hands-on
exercise built around a toy package called `relogio`.

| Section | Description |
|---|---|
| A importância do R | Why R matters for reproducible research and package-based work |
| CRAN | What CRAN is, why publish there, what it does and doesn't check |
| Como criar pacotes no R | Building a package skeleton, `DESCRIPTION`, `NAMESPACE`, `.Rd` docs, C/C++/Fortran code |
| O caminho até a publicação | Building, checking (`R CMD build` / `check --as-cran`), win-builder, and submitting to CRAN |
| Próximos passos | Maintaining, versioning, and promoting a package after acceptance |

Follow along using the [`package_example`](./package_example) folder, and
compare against [`package_example_answer`](./package_example_answer) if you
get stuck or want to see a filled-in reference.

## Package layout

- `slides.pdf` — the guide itself
- `package_example/` — starting point for the exercise: `build_package_skeleton.R` and the functions to package (`funcoes/minhas_funcoes.R`)
- `package_example_answer/` — a completed reference package (`relogio`) with `DESCRIPTION`, `NAMESPACE`, `R/`, and `man/` filled in

## References

- *Writing R Extensions*.
  <https://cran.r-project.org/doc/manuals/r-release/R-exts.html>
- Package **bgev** (Cira Otiniano, Yasmin Lírio e Thiago Sousa).
  <https://cran.r-project.org/package=bgev>
- Package **GEVStableGarch** (Thiago Sousa e Cira Otiniano).
  <https://cran.r-project.org/src/contrib/Archive/GEVStableGarch/>
- The R logo is © 2016 The R Foundation, used under CC-BY-SA 4.0.
  <https://www.r-project.org/logo.html>
