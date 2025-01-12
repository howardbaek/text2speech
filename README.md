
<!-- README.md is generated from README.Rmd. Please edit that file -->

# text2speech

<!-- badges: start -->

[![Travis build
status](https://travis-ci.com/muschellij2/text2speech.svg?branch=master)](https://travis-ci.com/muschellij2/text2speech)
[![AppVeyor build
status](https://ci.appveyor.com/api/projects/status/github/muschellij2/text2speech?branch=master&svg=true)](https://ci.appveyor.com/project/muschellij2/text2speech)
[![CRAN
status](https://www.r-pkg.org/badges/version/text2speech)](https://cran.r-project.org/package=text2speech)
<!-- badges: end -->

The goal of text2speech is to unify different text to speech engines,
such as Google, Microsoft, and Amazon.

## Installation

You can install the GitHub version of `text2speech`:

``` r
devtools::install_github("jhudsl/text2speech")
```

``` r
library(text2speech)
```

## Authentication

This should allow for authentication, which still needs to be set up in
each service separately, to be one function at least:

``` r
tts_auth("google")
tts_auth("amazon")
tts_auth("microsoft")
```

## Voices

Listing out different voices for each service.

``` r
df = tts_voices(service = "microsoft")
print(head(df))

if (tts_google_auth()) {
  df = tts_voices(service = "google")
  print(head(df))
}
if (tts_amazon_auth()) {
  df = tts_voices(service = "amazon")
  print(head(df))
}
if (tts_microsoft_auth()) {
  df = tts_voices(service = "microsoft")
  print(head(df))
}
```
