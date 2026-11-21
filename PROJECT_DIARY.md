# Music Discovery Research — Project Diary

A running record of progress, decisions, and the next step. Dates use America/Los_Angeles. Earlier entries were reconstructed from the project conversation and Git history; commit dates may differ from when work began.

## Current position — November 21, 2026

- **Working sample:** 68 track entries with release dates between January 1 and September 1, 2026, inclusive. All have ISRCs, with no repeated ISRCs within this filtered sample.
- **Working tables:** `tracks_df` contains all 100 entries; `album_df` holds their expanded album metadata and converted release dates. `filtered_album_df` and `filtered_tracks_df` contain the matching 68 entries, linked by their retained indexes.
- **Next step:** Inspect the `artists` lists, create a table of track–artist credits, and count unique artist IDs including collaborators. Artist counting has not yet been implemented in the saved notebook.
- **Still unresolved:** These are search-selected release entries, not a representative census or verified first releases of recordings. Public stream observations have not been collected, so the under-1,000 question is still pending.

## November 21, 2026 — Resuming and recording progress

- Reviewed the current position: 68 entries within the window, converted release dates in the album table, and no repeated ISRCs in the filtered track table. Selected unique artist counting as the next research task.
- Created this diary to keep daily progress and the next action easy to find. No artist-counting code was added as part of the diary update.

## November 17, 2026 — Data preparation, dates, and duplicate checks

- Confirmed 100 entries and 15 original top-level columns with no top-level missing values. Clarified that `isna()` does not inspect inside dictionaries or lists, and that `json_normalize()` flattens structure rather than cleaning values.
- Expanded album dictionaries into `album_df`, inspected dates, and converted `release_date` with `pd.to_datetime(..., errors="coerce")`. Checked for failed or missing dates and kept validation focused on fields used in the research.
- Created `filtered_album_df` for the inclusive January 1–September 1 window: 68 entries qualified and 32 were later releases. Used the retained indexes to create the corresponding `filtered_tracks_df`; original tables remained available.
- Distinguished Spotify track IDs from ISRC recording identifiers. Extracted ISRCs into a new column before creating filtered copies, then checked missing ISRCs and duplicates. The 68-entry sample has no missing or repeated ISRCs.
- Organized notebook headings into inspection, preparation, study-window selection, and duplicates while preserving existing code and comments. The full dataset's shared ISRC belongs to two releases of “Confused,” one inside the window and one after it; filtering removes the later entry.
- Committed successive notebook checkpoints: `d91c283` (initial exploration), `c964ae2` (date validation and filtering), `dd3b321` (aligned filtered tracks), and `2451fe3` (EDA organization and ISRC extraction). Later notebook edits remain subject to their own review and commit.

## November 16, 2026 — Repository and notebook setup

- Initialized the project repository under `Documents/GitHub/music-discovery-research`. Created the README-only first commit: `d1f5cab` — `docs: define research mission and pilot scope`.
- Published the repository on GitHub and set its description and topics. Established the distinction between local commits and pushing them to GitHub; raw data remained untracked.
- Discussed an AI-assisted portfolio approach emphasizing research decisions, verification, and understanding. Decided to explore in a Jupyter notebook before extracting reusable Python functions.
- An initial generated EDA was too elaborate for the desired learning pace and was removed, preserving the opening research questions. Restarted incrementally: load JSON, create `tracks_df`, inspect structure, and check missing values.

## November 14, 2026 — Recovering the project and defining its mission

- Located the original project and all ten downloaded JSON files. Combined the batches without altering the source files; the combined file was subsequently renamed `100_edm_tracks.json`.
- Verified 100 distinct Spotify track IDs and 99 distinct ISRCs in the full dataset. Discussed reusable processing and reviewed the Music Metadata Engine and ETL Kit as related projects.
- Drafted a README covering research questions, scope, data requirements, counting rules, and limitations. Proposed reusable music processing in the Music Metadata Engine while keeping study-specific decisions in this project; no integration was implemented.
- Added a future question about whether strategic genre labeling in underserved categories affects discoverability. Recorded it as a hypothesis requiring evidence, alongside ambiguity and search indexing as alternative explanations.
- Reviewed the README, removed collaboration-specific instructions from the public document, and discussed neutral project-focused wording. Selected `music-discovery-research` as the repository name.

## November 1, 2026 — API setup and feasibility tests

- Defined an initial study of techno releases dated January 1–September 1, 2026, starting with about 100 tracks. Target fields included track and artist IDs, release dates, ISRCs, Spotify URLs, and eventual public stream observations.
- Created a Spotify developer app and used Terminal requests to authenticate, search, and retrieve track metadata. Also tested user authorization and reading an owned playlist; that playlist contained older music and served only as an access test.
- Investigated unexpectedly sparse techno search results through genre, year, and artist comparisons. A known Marcel Dettmann track was retrievable directly and by title, but disappeared when genre filters were added. Techno searches reported 61 matches for 2024, one for 2025, and none for 2026; these were query results, not actual release totals. FUTURE QUESTION: Does incorrect genre
- Broadened the pilot to EDM using `genre:"electronic dance music" year:2026`. Downloaded ten batches of ten entries. The folder timestamp `20261102T021833Z` is UTC and corresponds to November 1 in Los Angeles.
- Observed blank public play counts in the desktop app and web player. Kept “blank/not displayed” separate from a presumed under-1,000 classification because the meaning of every blank has not been verified.

## Diary maintenance

- Insert each new dated entry above the previous daily entry (newest first) on workdays summarizing completed work, important findings or decisions, and remaining questions. Keep entries brief and distinguish discussion from implementation.
- Update “Current position” when the working dataset or next action changes. Record commits when relevant, but do not treat a local commit as evidence of a successful push.
