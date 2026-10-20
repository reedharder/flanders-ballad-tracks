# Flanders Ballad Collection — extracted tracks

Source: [Helen Hartness Flanders Ballad Collection](https://archive.org/details/helenhartnessflanders), Middlebury College Special Collections & Archives. Released CC BY — reuse with attribution.

This is the **data output** of a track-splitting/restoration pipeline being developed against the
collection's archive.org holdings (426 digitized items, ~220 hours). It currently holds 173
individual tracks: 171 pulled from 81 wax cylinders where the cylinder's own band files map
cleanly 1:1 onto its described song list, plus 2 tracks manually split out of a continuous,
medley-heavy cassette-tape reel as a proof of concept. Every track ships as both an unfiltered
original and a spectrally-denoised copy (noise profile estimated automatically per track; the
unfiltered original is always the primary/reference copy, never replaced).

`manifest.json` carries full structured metadata per track: title (display-cased, with the raw
transcription preserved), performer, location (+ geocoded coordinates), genre/instrumentation
(confirmed via [Traditional Tune Archive](https://tunearch.org) lookups where found, otherwise
clearly labeled as a heuristic guess or "uncertain" — most of this batch has no reliable
instrument signal at all, since the collection's one real metadata source for that only covers a
different subset of the archive), version-grouping (repeat performances of the same title), and
provenance notes (parser corrections, short-clip flags, etc).

## Folder guide

- **`confident/`, `confident_batch/`** — single song, correctly bounded, correctly labeled.
  Play in any standard audio player; ID3 tags (title/artist/album) are embedded. `_denoised.mp3`
  siblings are the filtered copies.
- **`pending_label/`** — cleanly split audio (no internal gap, so the *boundaries* are right),
  but which of a short list of remaining titles it is isn't resolved yet — see `candidates` in
  `manifest.json`.
- **`needs_qa/`** — boundaries themselves are uncertain (medley-heavy tape sides, ambiguous
  cylinder bands). Includes low-bitrate preview copies where the archival-quality source is
  still only on archive.org pending confirmed cuts.

## Known rough edges (being worked on)

- Most instrument/genre labels are unverified heuristics, not confirmed metadata — see each
  track's `genre.confidence` field.
- A handful of tracks run under 10 seconds with real (non-silent) audio content — likely
  damaged-cylinder partial recoveries or intentionally brief fragments, flagged in
  `duration_flag` rather than silently trusted.
- Title parsing has been corrected for a number of known OCR/regex issues but hasn't been
  exhaustively re-verified against every source description.

## Provenance

Every file traces back to a specific archive.org item - see `source_url` in `manifest.json`.
The processing pipeline/codebase lives in a companion repository (currently private while still
under active development).
