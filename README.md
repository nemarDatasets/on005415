[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on005415-blue)](https://doi.org/10.82901/nemar.on005415)

Welcome to the numbers dataset. These data were collected using stereoelectroencephalography recordings of epilepsy patients while they were waiting on the epilepsy monitoring unit to have seizures at Oregon Health & Science University. They were shown auditory and visual numbers that were symbolic (Arabic + spoken) or non-symbolic (dots + beeps).

## Channel names follow the data headers (18 Oct 2026)

In 13 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count), so `mne_bids.read_raw_bids` stopped with 'Channel mismatch' (or 'Duplicate channel names'); EEGDash renamed the data channels by position to the channels.tsv names, which gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 2744 rows took the header name (the header labels carry '-20000' suffix, '-2000' suffix).

electrodes.tsv is unchanged: it names the contacts (e.g. `A1`), while channel names follow the recorder (e.g. `A1-AV`); to attach positions in MNE, map channel names to contact names first, e.g. `raw.rename_channels(lambda n: re.sub(r'-[A-Za-z0-9]+$', '', n))`.
