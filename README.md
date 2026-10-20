# Flanders Ballad Collection — extracted tracks (prototype batch)

Source: [Helen Hartness Flanders Ballad Collection](https://archive.org/details/helenhartnessflanders), Middlebury College Special Collections & Archives. Released CC BY — reuse with attribution.

This folder holds the first real output of the track-splitting pipeline: two archive.org items
(`hhfbc-cyl67`, a wax cylinder; `hhfbc_tapes_D61A`, a cassette dub of a disc-recording reel) run
through automated segmentation and sorted into three confidence tiers. See `manifest.json` for
full structured metadata (titles, performers, locations, timestamps, archive.org links).

## Folder guide

- **`confident/`** — single song, correctly bounded, correctly labeled. Play these in any
  standard audio player; ID3 tags (title/artist/album) are already embedded.
- **`pending_label/`** — cleanly split audio (no internal gap, so the *boundaries* are right),
  but we don't yet know *which* of the remaining described songs each clip is — that depends on
  resolving the ambiguous clips below. Each file's `candidates` list in `manifest.json` narrows
  it to a handful of titles.
- **`needs_qa/`** — boundaries themselves are uncertain. Includes the two ambiguous cylinder
  bands at original quality, plus both sides of the D61A tape as low-bitrate (40kbps) *preview*
  copies — small enough to bundle in a browser tool, not intended as the final listening copy.
  The archival-quality source stays linked back to archive.org until a human confirms the cuts.

## Why some of this is unresolved

Energy/silence-based segmentation works when there's a real pause between songs. On this
material that's not reliable: performers were sometimes re-announced by a collector before
singing (creating a short, decoy "gap"), and fiddle medleys often run multiple tunes with *no*
gap at all. The pipeline flags duration outliers and multiple candidate pause points rather than
guessing — see the project report for the full writeup of this failure mode.

## Provenance

Every file traces back to a specific archive.org item and (for the needs-QA tier) a specific
timestamp range inside it — see `source_url` / `full_quality_url` in `manifest.json`.
