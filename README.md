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
npx clusterflick/scripts cache
```

This command:

- Reads the transformed cinema data
- Identifies unique movies that need metadata
- Fetches detailed information from The Movie Database API
- Stores the cached data for use in subsequent workflows

## Schedule

The workflow is automatically triggered when the
[data transformation workflow](https://github.com/clusterflick/data-transformed)
completes successfully. It can also be triggered manually via workflow dispatch
if needed.

## Maintenance

### Dependencies

The workflow requires API keys configured as GitHub secrets:

- `MOVIEDB_API_KEY` - For fetching movie metadata from The Movie Database
- `PAT` - Personal Access Token for triggering downstream workflows
