# Bronze Data Contract (v1)

## Purpose
Store a faithful, reproducible copy of CFPB complaint records ingested from the public source.

## Source
CFPB Consumer Complaint Database (public API).

## Refresh cadence (target)
Daily or 3x/week automated pull.

## Data retention window (initial)
Rolling last 24 months (configurable).

## Bronze invariants (rules)
1) No business transformations (no normalization, no derived columns).
2) Preserve source field names and values as received.
3) Append-only behavior preferred (new records added; existing records not modified unless source updates).
4) Each run logs: row count, min/max date_received, unique companies, column list.

## Output format
Parquet file(s) stored under data/bronze/.

## Output naming convention
complaints_raw_<YYYYMMDD>.parquet (optional versioning) OR complaints_raw.parquet (latest snapshot) with a separate run log.

## Known limitations
- Narrative text is missing for many records (consumer opt-in).
- Company names may be inconsistent; normalization occurs in Silver.
