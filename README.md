# YouTube Music Playlist Cleaner

A Google Colab-friendly Python utility for scanning YouTube Music playlists and removing playlist entries that match configurable cleanup rules.

## What it can remove

- Liked songs
- Disliked songs
- Songs shorter than a configured duration, default: under 2 minutes
- Songs longer than a configured duration, default: over 13 minutes
- Duplicate songs
- Unavailable songs

The script removes items from playlists. It does not delete songs from YouTube Music or YouTube itself.

## Safety model

The notebook runs in dry-run mode by default. In dry-run mode, it creates CSV reports showing exactly which playlist items would be removed. Actual deletion requires setting `DRY_RUN = False`.

Generated reports include:

- `all_tracks_*.csv`
- `deletion_plan_*.csv`
- `api_deletion_plan_*.csv`
- `skipped_missing_videoId_or_setVideoId_*.csv`
- `delete_responses_*.jsonl`

## Authentication

This project uses `ytmusicapi` browser authentication. You must copy raw request headers from your own authenticated YouTube Music browser session.

Never commit your real raw headers, cookies, authorization header, or generated `browser.json`.

See `docs/raw_headers_guide.md`.

## Usage in Google Colab

1. Open the notebook in Google Colab.
2. Install dependencies.
3. Paste your raw headers into the private notebook cell.
4. Keep `DRY_RUN = True`.
5. Run the scanner.
6. Review `deletion_plan_*.csv`.
7. Set `DRY_RUN = False` only after confirming the plan.
8. Run the deletion cell.

## Configuration

Important options:

- `PLAYLIST_IDS`
- `PLAYLIST_TITLE_CONTAINS`
- `DELETE_LIKED`
- `DELETE_DISLIKED`
- `DELETE_UNAVAILABLE`
- `DELETE_SHORTER_THAN_SECONDS`
- `DELETE_LONGER_THAN_SECONDS`
- `DELETE_DUPLICATES`
- `DUPLICATE_SCOPE`
- `DELETE_BATCH_SIZE`

## Limitations

This project uses an unofficial YouTube Music API wrapper. YouTube Music behavior may change. Authentication headers may expire. Playlist edits are destructive when dry-run mode is disabled.

## Disclaimer

This project is not affiliated with Google, YouTube, YouTube Music, or the `ytmusicapi` project. Use at your own risk. Review all dry-run reports before deleting playlist items.
