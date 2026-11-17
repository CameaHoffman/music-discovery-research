# Music Analytics Research

> Mission draft for review before implementation and the first commit.

## Mission

Develop a transparent, reproducible workflow for studying electronic dance music (EDM) releases on Spotify, beginning with a small feasibility study. Establish what can be reliably collected and measured before expanding the dataset or drawing conclusions about the wider music market.

The project also provides a practical research use case for reusable music-data processing in the Music Metadata Engine.

## Research questions

For releases dated **January 1 through September 1, 2026, inclusive**, I want to determine:

1. How many qualifying tracks can be identified through the documented collection method.
2. How many unique credited artists are associated with those tracks.
3. How many identified recordings have fewer than 1,000 all-time Spotify streams at the time of observation, if a reliable classification method can be established.
4. What percentage of the eligible sample falls below that threshold, with unknown cases reported separately.

All-time stream counts are measured as of observation, not as of the release-window cutoff. The separate rolling 12-month royalty eligibility threshold is outside this study.

## Initial scope (10.16.2026)

- **Music:** EDM, initially operationalized through Spotify search using `genre:"electronic dance music"`.
- **Release window:** January 1–September 1, 2026.
- **Catalog availability:** United States. The account used for collection is registered in the US.
- **Pilot size:** Approximately 100 raw search results, with potentially fewer eligible recordings after date checks and deduplication.
- **Sampling method:** Search-returned results, not a random or representative sample of all EDM releases.
- **Current phase:** Metadata collection and cleaning feasibility. No machine learning yet.

The scope began with techno. Tests showed that Spotify's techno genre filter excluded known examples and returned very few recent matches. Broader EDM searches returned results, but broader wording does not establish comprehensive coverage.

## What we have established

- Spotify API authentication, track lookup, search, and reading an owned playlist have worked in our tests.
- Ten JSON search batches were downloaded for `genre:"electronic dance music" year:2026`.
- Those batches were combined into a file subsequently named `100_edm_tracks.json`.
- The combined data contains 100 distinct Spotify track IDs and 99 distinct ISRCs, indicating a potential duplicate recording across releases.
- Cleaning and stream-display observations have not yet been completed.

The API's reported search total describes that query's results. It must not be presented as the total number of EDM releases on Spotify.

## Data to retain

For each source record, retain:

- Source and Spotify track ID.
- Track title and Spotify URL.
- Every credited artist's name and Spotify ID.
- Album or release ID, release date, and date precision.
- ISRC, when available.
- Collection query, market, source batch, and collection timestamp when known.
- Public play-count observation, observation date, and collection method when collected.
- Derived classification, its basis, and any uncertainty.

Keep original observations separate from derived values. Missing information must remain identifiable rather than being silently filled in.

## Cleaning and counting rules

1. Preserve the original downloaded files.
2. Standardize source-specific fields into a shared track-record structure.
3. Check required fields and report missing, invalid, or incomplete values.
4. Compare release dates against the inclusive study window. Flag dates whose precision prevents a confident decision.
5. Identify repeated track IDs and shared ISRCs. Preserve links to every source release when grouping recordings.
6. Count unique artists by Spotify artist ID, including collaborators.
7. Report raw entries, eligible release entries, deduplicated recordings, unique artists, exclusions, and unresolved cases separately.

An album's release date is not necessarily a recording's original release date. Reissues and compilations require an explicit inclusion rule before final research counts are produced. A missing ISRC must not cause unrelated records to be merged.

## Stream-count feasibility

Spotify's official Web API does not supply all-time track stream counts. During initial checks, some public play counts appeared blank in both the desktop app and web player.

The working hypothesis is that these blanks may indicate fewer than 1,000 streams, but it has not been verified that every blank has that meaning. Record **blank/not displayed** as the observation. Any **presumed under 1,000** classification must be clearly labeled as an assumption and reported separately from confirmed classifications.

Before calculating the final percentage, define the classification evidence, treatment of unknowns, and denominator. The feasibility study may conclude that this research question cannot yet be answered reliably with the available data.

## Relationship to existing projects

### Music Metadata Engine

Proposed home for reusable music-specific processing: a Spotify JSON importer, a standard track structure, release-date handling, and recording identity checks. Its current focus is CSV-based DJ-library metadata; extending it is a proposed next stage, not completed integration.

### ETL Kit

Provides a useful pattern: read, validate, separate accepted and rejected records, and save outputs. Its current name-and-age validation is not directly applicable to music records. Reuse the design where useful; a package dependency is not required at this stage.

### This research project

Owns the study questions, collection provenance, dataset snapshots, date-window configuration, stream observations, analysis, and limitations. Research-specific decisions should remain visible here even when reusable processing lives in another project.

## Future research question: genre labeling and discoverability

Investigate whether some artists, labels, or distributors strategically label releases in genres they perceive as underserved to improve visibility, and whether mismatches between labels and musical content make discovery less useful for listeners.

Treat this as a hypothesis, not an established explanation for search results. Distinguish intentional misrepresentation from reasonable genre overlap, inconsistent terminology, missing metadata, and Spotify's own classification or search indexing. An unexpected search result alone does not establish who assigned a genre or why.

Future work should define what “underserved” means, establish a consistent method for assessing genre fit, and seek evidence about how labels are assigned before making claims about intent. This question is exploratory and does not change the initial pilot's scope.

## Next steps

1. Review and edit this mission document, then approve it for the first commit.
2. Decide the standard track fields and original-release versus reissue policy.
3. Define the reusable processing function's inputs, outputs, and validation behavior.
4. Implement and test the smallest useful processing workflow against the pilot data.
5. Evaluate a reliable method for observing public stream displays.
6. Review feasibility findings before expanding collection.

