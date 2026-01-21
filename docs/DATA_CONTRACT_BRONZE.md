# Bronze Data Contract (v1)

## Purpose
Store a faithful, reproducible copy of CFPB complaint records ingested from the public source.  
Bronze data serves as the immutable audit layer for all downstream analytics, metrics, and models.

## Source
CFPB Consumer Complaint Database  
- Public API (preferred when reliable)
- Official bulk exports (fallback)

## Refresh cadence (target)
Daily or 3x/week automated pull.

## Retention policy (v1)
Rolling retention window: keep the last **N days** of data (default: 90 days).  
Older partitions are deleted automatically by the ETL job.

Retention window is configurable via ETL configuration and may be expanded once storage and performance characteristics are validated.

## Storage layout (partitioned)
Bronze data is stored partitioned by `date_received` to support efficient filtering, retention, and replay.

```text
data/bronze/
  date_received=YYYY-MM-DD/
    complaints_raw_<RUN_TS>.parquet
    run_meta_<RUN_TS>.json
