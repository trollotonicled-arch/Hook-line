# Hookline

A listening booth that learns your ear. It plays the best 15 seconds of a song from Apple Music; you keep it or toss it, and every vote retrains a small taste model in your browser.

**Play it:** https://trollotonicled-arch.github.io/Hook-line/

On iPhone, tap Share → Add to Home Screen and open it from there for true full screen.

## How it works

- **Catalogue:** Apple's iTunes genre charts (19 genres, ~1,700 tracks per store region), plus more songs from artists you keep, via the public iTunes Search API.
- **The hook:** each track's 30-second Apple preview is decoded in the browser. A worker computes loudness, onset density and low-end energy frame by frame and picks the strongest window (10/15/20 s or full), snapped to a transient.
- **Sound features:** the same pass measures energy, tempo (onset autocorrelation), tone (spectral centroid), bass ratio, punch, groove (beat regularity) and density.
- **Taste model:** online Bayesian logistic regression with a diagonal Gaussian posterior over genre, family, decade, artist and soft-binned sound features. Picks use tempered Thompson sampling, plus an occasional labelled "curveball" from a genre you haven't heard.
- **Privacy:** your votes and model live in `localStorage` on your device. The only network calls go to Apple (charts, previews, artwork) and Google Fonts.

## Keys

← toss · → keep · space pause · F full screen · R replay hook · P full preview · T your taste

Single file: everything is in `index.html`.
