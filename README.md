
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
#> [1] FALSE
tts_auth("amazon")
#> Warning in pollyHTTP(action = "voices", verb = "GET", query = query, ...):
#> Forbidden (HTTP 403).
#> Warning in structure(out[["Voices"]], NextToken = out[["NextToken"]]): Calling 'structure(NULL, *)' is deprecated, as NULL cannot have attributes.
#>   Consider 'structure(list(), *)' instead.
#> Warning in pollyHTTP(action = "voices", verb = "GET", query = query, ...):
#> Forbidden (HTTP 403).
#> Warning in structure(out[["Voices"]], NextToken = out[["NextToken"]]): Calling 'structure(NULL, *)' is deprecated, as NULL cannot have attributes.
#>   Consider 'structure(list(), *)' instead.
#> [1] FALSE
tts_auth("microsoft")
#> Error in ms_get_tts_key(api_key = api_key, error = TRUE) : 
#>   MS API key not found, please set option('ms_tts_key') for general use or set environment variable MS_TTS_API_KEY, to be accessed by Sys.getenv('MS_TTS_API_KEY')
#> [1] FALSE
```

## Voices

Listing out different voices for each service.

``` r
df = tts_voices(service = "microsoft")
print(head(df))
#>                                                                 voice
#> 2          Microsoft Server Speech Text to Speech Voice (ar-EG, Hoda)
#> 3   Microsoft Server Speech Text to Speech Voice (ar-EG, SalmaNeural)
#> 1  Microsoft Server Speech Text to Speech Voice (ar-EG, ShakirNeural)
#> 4 Microsoft Server Speech Text to Speech Voice (ar-SA, ZariyahNeural)
#> 5         Microsoft Server Speech Text to Speech Voice (ar-SA, Naayf)
#> 6   Microsoft Server Speech Text to Speech Voice (ar-SA, HamedNeural)
#>                language language_code gender   service
#> 2       Arabic (Arabic)         ar-EG Female microsoft
#> 3       Arabic (Arabic)         ar-EG Female microsoft
#> 1       Arabic (Arabic)         ar-EG   Male microsoft
#> 4 Arabic (Saudi Arabia)         ar-SA Female microsoft
#> 5 Arabic (Saudi Arabia)         ar-SA   Male microsoft
#> 6 Arabic (Saudi Arabia)         ar-SA   Male microsoft

if (tts_google_auth()) {
  df = tts_voices(service = "google")
  print(head(df))
}
if (tts_amazon_auth()) {
  df = tts_voices(service = "amazon")
  print(head(df))
}
#> Warning in pollyHTTP(action = "voices", verb = "GET", query = query, ...):
#> Forbidden (HTTP 403).
#> Warning in structure(out[["Voices"]], NextToken = out[["NextToken"]]): Calling 'structure(NULL, *)' is deprecated, as NULL cannot have attributes.
#>   Consider 'structure(list(), *)' instead.
#> Warning in pollyHTTP(action = "voices", verb = "GET", query = query, ...):
#> Forbidden (HTTP 403).
#> Warning in structure(out[["Voices"]], NextToken = out[["NextToken"]]): Calling 'structure(NULL, *)' is deprecated, as NULL cannot have attributes.
#>   Consider 'structure(list(), *)' instead.
if (tts_microsoft_auth()) {
  df = tts_voices(service = "microsoft")
  print(head(df))
}
#> Error in ms_get_tts_key(api_key = api_key, error = TRUE) : 
#>   MS API key not found, please set option('ms_tts_key') for general use or set environment variable MS_TTS_API_KEY, to be accessed by Sys.getenv('MS_TTS_API_KEY')
```
