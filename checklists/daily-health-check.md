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

## ✅ 2. Indexer / Ingestion Health

### Check 3: Indexing Throughput
```spl
index=_internal source=*metrics.log group=thruput
| timechart sum(kb) by series
```

### Check 4: Parsing & Indexing Queues
```spl
index=_internal source=*metrics.log group=queue
| timechart avg(current_size) by name
```

## ✅ 3. License Usage
```spl
index=_internal sourcetype=splunkd component=LicenseUsage
| stats sum(b) as bytes by idx
```

📌 Notes

Helps detect ingestion delays early

Ensures searches are running normally

Aligns with Splunk Support best practices
