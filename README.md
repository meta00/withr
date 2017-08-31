<!-- README.md is generated from README.Rmd. Please edit that file -->
Withr - Run Code 'With' Modified State
======================================

[![Travis-CI Build Status](https://travis-ci.org/r-lib/withr.svg?branch=master)](https://travis-ci.org/r-lib/withr) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/r-lib/withr?branch=master&svg=true)](https://ci.appveyor.com/project/jimhester/withr) [![Coverage status](https://codecov.io/gh/r-lib/withr/branch/master/graph/badge.svg)](https://codecov.io/github/r-lib/withr?branch=master) [![CRAN Version](http://www.r-pkg.org/badges/version/withr)](http://www.r-pkg.org/pkg/withr)

A set of functions to run code 'with' safely and temporarily modified global state. There are two sets of functions, those prefixed with `with_` and those with `local_`. The former reset their state as soon as the `code` argument has been evaluated. The latter reset when they reach the end of their scope, usually at the end of a function body.

Many of these functions were originally a part of the [devtools](https://github.com/hadley/devtools) package, this provides a simple package with limited dependencies to provide access to these functions.

-   `with_collate()` / `local_collate()` - collation order
-   `with_dir()` / `local_dir()` - working directory
-   `with_envvar()` / `local_envvar()` - environment variables
-   `with_libpaths()` / `local_libpaths()` - library paths
-   `with_locale()` / `local_locale()` - any locale setting
-   `with_makevars()` / `local_makevars()` - Makevars variables
-   `with_options()` / `local_options()` - options
-   `with_par()` / `local_par()` - graphics parameters
-   `with_path()` / `local_path()` - PATH environment variable

There are also `with_()` and `local_()` functions to construct new `with_*` and `local_*` functions if needed.

``` r
dir.create("test")
getwd()
#> [1] "/private/var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T/Rtmp5eQ5oF"
with_dir("test", getwd())
#> [1] "/private/var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T/Rtmp5eQ5oF/test"
getwd()
#> [1] "/private/var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T/Rtmp5eQ5oF"
unlink("test")

Sys.getenv("WITHR")
#> [1] ""
with_envvar(c("WITHR" = 2), Sys.getenv("WITHR"))
#> [1] "2"
Sys.getenv("WITHR")
#> [1] ""

with_envvar(c("A" = 1),
  with_envvar(c("A" = 2), action = "suffix", Sys.getenv("A"))
)
#> [1] "1 2"
```

See Also
========

-   [Devtools](https://github.com/hadley/devtools)
