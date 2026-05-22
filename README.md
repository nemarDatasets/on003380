[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on003380-blue)](https://doi.org/10.82901/nemar.on003380)

This sedation, ischemia, recovery experiment contains 11 animals (juvenile pigs).

Animals were surgically instrumented, and then monitored under sedation states 1-5 (isoflurane, fentanyl, propofol), followed by 1 or 2 episodes of gradual ischemia (states 6 and 8) and recovery (recovery 1 = state 7, between state 6 and 8; recovery 2, after state 8, corresponding to states 9-12).

Two crude groups are indicated: 
1) sedation - animals had no ischemia and 
2) ischemia - animals had sedation, followed by ischemia episodes and followed by recovery.

The scientific article (see Reference) contains all methodological details.
- Martin Frasch and Reinhard Bauer, October 2, 2020

PS. Sub-12 folder is to be ignored. It was added to satisfy the BIDS validation algorithm.

## NEMAR curation changes (2026-05-21, revised 2026-05-22)

Raw binary payloads (`.edf`, `.tar.gz`) are byte-identical. Final BIDS-validator state: 0 errors.

### `dataset_description.json`
- Added `DatasetType: "raw"`.
- Added `GeneratedBy: [{Name: "nemar-cli", Version: "0.8.8", CodeURL: "https://github.com/nemar-org/nemar-cli"}]`.
- Bumped `BIDSVersion` `1.1.1` → `1.8.0`.

### `.bidsignore`
- Added `sub-12`, `sub-12/`, `sub-12/**` (multiple unanchored patterns to cover both the directory entry and its contents). Why: per the dataset's own README, "Sub-12 folder is to be ignored. It was added to satisfy the BIDS validation algorithm." Excluding `sub-12/` from validation makes the placeholder no longer trigger BIDS-validator errors. The original `sub-12/eeg/sub-12_eeg.edf` symlink and `channels.tsv` are preserved unchanged.

The other 11 subject directories (`sub-01` through `sub-11`) and their `channels.json` / `channels.tsv` files are untouched. They carry the study's documented per-subject metadata but no `_eeg.edf` (the dataset's published structure on OpenNeuro keeps the EEG data inside `sub-NN_edf.tar.gz` archives, which are excluded from validation by the existing `.bidsignore` pattern `*_edf.tar.gz`).
