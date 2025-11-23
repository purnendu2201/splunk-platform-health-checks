# Weekly Health Review – Splunk Platform


### 🎯 Purpose

A deeper platform review to detect trends, noise, or hidden issues.

---

## 🔍 1. Top Indexes by Volume

```spl
| tstats sum(_raw) as bytes where index=* by index
| eval gb=round(bytes/1024/1024/1024,2)
```

🔍 2. Data Latency Review
```spl
index=_internal sourcetype=metrics group=per_sourcetype_thruput
| timechart avg(ingest_latency)
```

🔍 3. App & Add-on Health

- Check for misconfigured dashboards
- Validate field extractions
- Validate sourcetype assignments

🔍 4. Review Alert Noise

- Identify noisy alerts
- Tune thresholds
- Adjust suppression windows

### 📌 Notes

Weekly checks help identify slow-burning issues such as increasing delays, rising volumes, or misconfigurations.
