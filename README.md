[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on003380-blue)](https://doi.org/10.82901/nemar.on003380)

This sedation, ischemia, recovery experiment contains 11 animals (juvenile pigs).

Animals were surgically instrumented, and then monitored under sedation states 1-5 (isoflurane, fentanyl, propofol), followed by 1 or 2 episodes of gradual ischemia (states 6 and 8) and recovery (recovery 1 = state 7, between state 6 and 8; recovery 2, after state 8, corresponding to states 9-12).

Two crude groups are indicated: 
1) sedation - animals had no ischemia and 
2) ischemia - animals had sedation, followed by ischemia episodes and followed by recovery.

The scientific article (see Reference) contains all methodological details.
- Martin Frasch and Reinhard Bauer, October 2, 2020

PS. Sub-12 folder is to be ignored. It was added to satisfy the BIDS validation algorithm.

## NEMAR curation changes (2026-05-21, revised 2026-05-27)

The BIDS validator went from 6 errors + 29 warnings to 0 errors + 2 warnings. None of the raw `.edf` files were modified, every change is to a text sidecar.

**Dataset description (`dataset_description.json`)**
- Added `DatasetType: "raw"` so the dataset is validated as raw data rather than a derivative.
- Updated `BIDSVersion` from `1.1.1` to `1.11.1` (the version the current validator checks against).
- `GeneratedBy` was left absent, exactly as the source published it, nothing was added there.

**Validator-ignore list (`.bidsignore`)**
- Added entries that exclude the `sub-12` directory from validation (`sub-12`, `sub-12/`, `sub-12/**`, covering both the directory entry and everything inside it). The dataset's own README explains that `sub-12` is a placeholder folder added only to satisfy an older BIDS-validator quirk, so it was never a real subject. Excluding it cleans up the errors and warnings the current validator raises against that placeholder (a missing task entity in the EDF filename, missing required sidecar keys like `TaskName`, `SamplingFrequency`, `PowerLineFrequency`, `EEGReference`, `SoftwareFilters`, and a long list of recommended-but-missing fields). The placeholder files themselves (`sub-12/eeg/sub-12_eeg.edf` symlink and `sub-12/eeg/channels.tsv`) are preserved unchanged.

**Other subject directories (`sub-01` through `sub-11`)**
- Untouched. Their `channels.json` and `channels.tsv` files carry the study's documented per-subject metadata, and they are not flagged by the validator because the existing `.bidsignore` entry `*_edf.tar.gz` already excludes the per-subject EEG archives from validation (see the next section for why the EEG payloads live in archives rather than loose `.edf` files).

**Remaining warnings (2), left on purpose**
- `HEDVersion` and `GeneratedBy` in `dataset_description.json` are flagged as recommended-but-missing. Neither was added: the dataset does not use HED tags, and `GeneratedBy` was deliberately left off (see the dataset-description bullet above).

**Out of mechanical scope: per-subject EEG packaging**
- The published dataset stores each subject's EEG recording inside a `.tar.gz` archive at `sub-NN/eeg/sub-NN_edf.tar.gz` rather than as a loose `.edf` file. That packaging matches the source on OpenNeuro and is what the dataset's existing `.bidsignore` rule `*_edf.tar.gz` is there to silence. Unpacking the archives into BIDS-canonical `sub-NN_task-..._eeg.edf` files would require deciding on a task slug, generating a matching `_eeg.json` for each recording, and verifying the contents against the publication, which is a study-level call rather than a mechanical sidecar fix, so it was left alone.
