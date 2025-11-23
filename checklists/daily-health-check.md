# Daily Health Check – Splunk Platform

### 🎯 Purpose
A quick daily review to ensure Splunk Cloud / Enterprise is healthy and performing normally.

---

## ✅ 1. Search Head Health

### Check 1: Skipped Searches
```spl
index=_internal sourcetype=scheduler status=skipped
| stats count by savedsearch_name
```
### Check 2: Search Lag
```spl
index=_internal sourcetype=search_metrics
| stats avg(scan_time) avg(event_count)
```

