# data-cached

This repository contains the automated workflow for caching MovieDB data for the
Clusterflick project.

## Purpose

The caching workflow retrieves and stores movie metadata from The Movie Database
(TMDB) for all movies identified in the transformed cinema data. This cached
data improves performance and reduces API calls in downstream processes.

## How It Works

The workflow executes the cache command to build a local cache of movie
metadata:

```bash
npm run cache
```

This command:

- Reads the transformed cinema data
- Identifies unique movies that need metadata
- Fetches detailed information from The Movie Database API
- Stores the cached data for use in subsequent workflows

## Schedule

The workflow is automatically triggered when the
[data diffing workflow](https://github.com/clusterflick/data-diffed) completes,
which is itself triggered by
[data transformation](https://github.com/clusterflick/data-transformed). Running
after the diff rather than beside it means the seen registry it reads describes
the same release it is about to cache. It can also be triggered manually via
workflow dispatch if needed.

## Downstream Triggers

After successfully caching the data, this workflow triggers:

- [data-combined](https://github.com/clusterflick/data-combined) - To combine
  all venue data into a unified dataset

## Maintenance

### Dependencies

The workflow requires API keys configured as GitHub secrets:

- `MOVIEDB_API_KEY` - For fetching movie metadata from The Movie Database
- `PAT` - Personal Access Token for triggering downstream workflows

## Licence

The code in this repository is licensed under the [MIT licence](LICENSE).

The releases are **not licensed at all**. They are film metadata retrieved from
The Movie Database and cached for the pipeline's use — synopses, cast and crew,
release dates, poster paths, genres and trailer ids. Almost none of it is
Clusterflick's own work: it belongs to TMDB, is used under the
[TMDB API terms of use](https://www.themoviedb.org/api-terms-of-use), and cannot
be sublicensed. If you want this metadata, get it from TMDB under your own API
terms.

For data you can use, see the
[data licence](https://clusterflick.com/data-licence). The exact terms for this
repository are in [LICENSE-DATA](LICENSE-DATA).
