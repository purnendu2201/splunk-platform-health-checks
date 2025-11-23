# Scheduler Health (Saved Search Monitoring)

## 🎯 Purpose
Monitor saved searches, alert failures, and overall scheduler performance.

---

### 🔧 1. Skipped Searches

```spl
index=_internal sourcetype=scheduler status=skipped
| stats count by savedsearch_name
```

### 🔧 2. Long-Running Searches

```spl
index=_audit action=search info=completed
| where duration>30
| stats avg(duration) max(duration) by user
```

### 🔧 3. Failed Alerts

```spl
index=_internal sourcetype=scheduler status=error
| stats count by savedsearch_name error_message
```

## 📌 Notes

This helps maintain visibility over alert reliability and scheduled job performance.
