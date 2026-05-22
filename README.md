[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on003380-blue)](https://doi.org/10.82901/nemar.on003380)

This sedation, ischemia, recovery experiment contains 11 animals (juvenile pigs).

Animals were surgically instrumented, and then monitored under sedation states 1-5 (isoflurane, fentanyl, propofol), followed by 1 or 2 episodes of gradual ischemia (states 6 and 8) and recovery (recovery 1 = state 7, between state 6 and 8; recovery 2, after state 8, corresponding to states 9-12).

Two crude groups are indicated: 
1) sedation - animals had no ischemia and 
2) ischemia - animals had sedation, followed by ischemia episodes and followed by recovery.

The scientific article (see Reference) contains all methodological details.
- Martin Frasch and Reinhard Bauer, October 2, 2020

PS. Sub-12 folder is to be ignored. It was added to satisfy the BIDS validation algorithm.

## NEMAR curation changes (2026-05-21)

BIDS validator: 6 errors + 28 warnings → 0 errors + 14 warnings. The `sub-12_eeg.edf` binary payload is unchanged (only the symlink was renamed via `git mv`).

### `dataset_description.json`
- Added `DatasetType: "raw"`.
- Added `GeneratedBy: [{Name: "nemar-cli", Version: "0.8.8", CodeURL: "https://github.com/nemar-org/nemar-cli"}]`.
- Bumped `BIDSVersion` `1.1.1` → `1.8.0`.

### `sub-12/eeg/` filename rename (task entity)
- `sub-12_eeg.edf` → `sub-12_task-sedationIschemiaRecovery_eeg.edf`
- `channels.tsv` → `sub-12_task-sedationIschemiaRecovery_channels.tsv`
- Task slug derived from the existing `TaskName: "sedation, ischemia, recovery"` already documented in every `sub-NN/eeg/sub-NN_channels.json` sidecar. Closes the `MISSING_REQUIRED_ENTITY` error.

### `sub-12/eeg/sub-12_task-sedationIschemiaRecovery_eeg.json` (new)
- Created using only values already documented in the dataset (the eleven byte-identical `sub-NN/eeg/sub-NN_channels.json` sidecars carry the study-level constants) and verified from the EDF header. Closes the 5 `SIDECAR_KEY_REQUIRED` errors.
- Required keys: `TaskName: "sedation, ischemia, recovery"`, `SamplingFrequency: 2000` (EDF-verified), `PowerLineFrequency: 50`, `EEGReference: "Cz"`, `SoftwareFilters: "n/a"`.
- Recommended keys (all from existing per-subject sidecars or EDF): `RecordingType: "continuous"`, `RecordingDuration: 322` (computed from EDF: 644000 samples / 2000 Hz; supersedes the stale `300` written in the per-subject sidecars), `EEGChannelCount: 9`, `ECGChannelCount/EOGChannelCount/EMGChannelCount/MISCChannelCount/TriggerChannelCount: 0` (matching the 9-row `channels.tsv`), `EEGPlacementScheme: "10-20"` (inferred from channel names — T5/T6 are 10-20 labels), `Manufacturer: "GJB Datentechnik"`, `ManufacturersModelName: "GJB Datentechnik Bolten & Jannek GbR, Ilmenau, Germany"`, `InstitutionName: "Jena University Hospital"`, `InstitutionAddress: "Hans Knoell Str. 2, Floor 3, D-07745 Jena, Germany"`, `InstitutionalDepartmentName: "Institute of Molecular Cell Biology"`.

### `sub-12/eeg/sub-12_task-sedationIschemiaRecovery_channels.tsv`
- 9 rows preserved, channel names (`Fp1`, `Fp2`, `F4`, `C3`, `C4`, `T5`, `T6`, `P3`, `P4`) and units (`uV`) unchanged.
- `type` column changed from prose strings (`ECoG frontal left`, etc.) to BIDS-canonical `EEG` for all 9 rows (closes `TSV_VALUE_INCORRECT_TYPE`).
- The original prose moved into `description` (which previously held EDF channel indices 6–14); the index information was not BIDS-canonical and is dropped.
- Original typo `cenral` (row C4) preserved verbatim — left as a separate concern.

The other 11 subject directories (`sub-01` through `sub-11`) and their `channels.json` / `channels.tsv` files are untouched. They carry the study's documented per-subject metadata but no `_eeg.edf` (the dataset's published structure on OpenNeuro).
