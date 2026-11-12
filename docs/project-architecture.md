# Project Architecture

## Climate analytics pipeline

```mermaid
flowchart TD
    A[Annual compressed weather files] --> B[Explicit daily schema]
    C[Fixed-width metadata files] --> D[Typed station and inventory tables]
    B --> E[Distinct station IDs and bounded aggregates]
    D --> F[Enriched station table]
    E --> G[Bidirectional coverage validation]
    F --> G
    B --> H[Station-year and country-year summaries]
    F --> H
    H --> I[Temperature and precipitation figures]
```

## Music ML pipeline

```mermaid
flowchart TD
    A[Audio attribute definitions] --> B[Generated Spark schemas]
    C[Distributed audio features] --> D[Validated feature families]
    B --> D
    D --> E[Joined track feature table]
    E --> F[Variance and correlation screening]
    F --> G[Binary and multiclass classifiers]
    H[Taste Profile interactions] --> I[Iterative support filtering]
    I --> J[Integer user and song mappings]
    J --> K[Warm-start split]
    K --> L[Implicit ALS]
    L --> M[Precision NDCG and MAP at 10]
```

## Shared design principles

- Inspect storage metadata before scanning large files.
- Make observational grain explicit before joining.
- Validate identifiers, nulls, duplicates, and coverage before modelling.
- Fit preprocessing only on training data.
- Check class balance before selecting metrics.
- Aggregate in Spark and collect only bounded results for plotting.
- Treat cloud checkpoints and cached intermediates as execution tools, not public repository assets.

