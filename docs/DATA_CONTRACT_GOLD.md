# Gold Data Contract — Trust Radar Aggregates (v1)

## Purpose
Executive-ready aggregates derived from Silver for fast dashboarding and monitoring.

## Source
Silver partitions:
data/silver/date_received=YYYY-MM-DD/complaints_silver_<RUN_TS>.parquet

## Outputs (v1)

### gold_daily_company_product.parquet
Grain: day × company_clean × product
Metrics:
- complaints_count
- timely_rate
- dispute_rate

### gold_issue_heatmap.parquet
Grain: company_clean × issue (optionally product)
Window: last N days (configurable)
Metrics:
- complaints_count
- share_of_company_complaints

### gold_spike_signals.parquet
Grain: day × company_clean × issue
Metrics:
- complaints_count
- baseline_mean (rolling)
- baseline_std (rolling)
- z_score
- spike_flag

## Storage layout
data/gold/
  gold_daily_company_product_<RUN_TS>.parquet
  gold_issue_heatmap_<RUN_TS>.parquet
  gold_spike_signals_<RUN_TS>.parquet
  run_meta_<RUN_TS>.json

## Notes
- Gold is small and optimized for BI/dashboard reads.
- No row-level complaint text needed in Gold v1.
