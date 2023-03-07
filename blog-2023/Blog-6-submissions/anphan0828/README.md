renv 101
================
An Phan
2023-03-02

<!-- README.md is generated from README.Rmd. Please edit that file -->
<!-- badges: start -->

[![Frontmatter
check](../../actions/workflows/check-yaml.yaml/badge.svg)](../../actions/workflows/check-yaml.yaml)
[![Render
rmarkdown](https://github.com/Stat585-at-ISU/blog-4-anphan0828/actions/workflows/render-rmarkdown.yaml/badge.svg)](https://github.com/Stat585-at-ISU/blog-4-anphan0828/actions/workflows/render-rmarkdown.yaml)
<!-- badges: end -->

What happens when we change the Rmd file and commit?

In Blog 5 you had the first exposure to Github Actions. We just checked
frontmatter compliance (as we do for this round). You see that we have
added a second action - here, we are converting the Rmarkdown document
to a markdown file by running `render_rmarkdown` on Github. This action
passes successfully for this document. We want to do something similar
for blog \#4.

Now start reading …

Read the vignette [Introduction to
renv](https://rstudio.github.io/renv/articles/renv.html) for the `renv`
R package by Kevin Ushey.

Then do:

1.  **Install the R package `renv` on your local machine.**

``` r
suppressWarnings(suppressMessages(install.packages("renv")))
#> Installing renv [0.17.0] ...
#>  OK [linked cache in 0.33 milliseconds]
#> * Installed 1 package in 8.8 milliseconds.
suppressWarnings(suppressMessages(library(renv)))
```

Run the command `usethis::use_github_action("render-rmarkdown.yaml")`

2.  **In the project for blog 4, initialize the workflow used by the
    `renv` package.**

Use `renv::init()`

3.  **Add all dependencies to the environment (implicitly by installing
    all the dependencies or explicilty by listing dependencies in a
    DESCRIPTION file).**

Use `renv::dependencies()` and copy to DESCRIPTION file

4.  **Add the `renv` folder to your blog 4 repository, and push the
    changes.**

Added and pushed
[here](https://github.com/Stat585-at-ISU/blog-4-anphan0828)

5.  **Is the github action working? Read any potential error messages in
    the workflow and try to fix things. Make sure to check stackoverflow
    for help, don’t forget our Discussion board!**

Not yet, have to change the
[path](https://github.com/Stat585-at-ISU/blog-4-anphan0828/actions/workflows/render-rmarkdown.yaml)
of `render-rmarkdown` badge to blog-4 instead of blog-6.

Write a blog post addressing the following questions:

1.  **What is the idea of the renv package?**

`renv` stands for R environment, which is a library manager where the
packages and versions are keeping track of to make sure an R environment
stays the same, no matter how the versions and updates change. This is
useful for robustness and reproducibility because we do not need to
manually fix the code to adapt with new updates, but rather use an old R
environment that had worked before.

2.  **In 50 to 100 words describe your experience working with `renv`.
    What went well? What did not go so well?**

Unfortunately, `renv` was giving me a hard time. Two main problems that
occurred to me:

- When I used `renv::snapshot()`, `curl` was added in `renv.lock` even
  though it is not one of the dependencies. And th GitHub action
  `render-rmarkdown` makes it messy, because a step called **Run
  <r-lib/actions/setup-renv@v2>** attempted to install everything in
  `renv.lock` including `curl`. This keeps failing and eventually I ran
  `renv::remove("curl")` to escape this mess. But I need to find
  solution for this in the future in case `curl` is a dependency.
- When I changed the path of the `render-rmarkdown` action in blog-6 to
  the file in blog-4, I am not sure if this is what I am supposed to do.
  Prof. Hofmann told us to re-address this action because blog-4 is our
  main focus, if I understood correctly. One warning was raised in the
  `render-rmarkdown` of
  [blog-4](https://github.com/Stat585-at-ISU/blog-4-anphan0828/actions/runs/4320159859/jobs/7540110286)
  is **Warning: Could not fetch resource
  ../../actions/workflows/render-rmarkdown.yaml/badge.svg** which I am
  not sure how to deal with.