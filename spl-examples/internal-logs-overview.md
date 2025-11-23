# Internal Logs Overview (SPL Examples)

## 🎯 Purpose

Understand Splunk internal processes by reviewing `_internal` and `_introspection` indexes.

---

### 🔧 1. Error Frequency

```spl
index=_internal log_level=ERROR OR log_level=WARN
| stats count by log_level component
```

### 🔧 2. Monitoring Queue Activity

```spl
index=_internal source=*metrics.log group=queue
| timechart avg(current_size) by name
```

### 🔧 3. Indexing Delay / Pipeline Latency

```spl
index=_internal sourcetype=metrics group=pipeline
| timechart avg(exec_time) by processor
```

## 📌 Notes

These SPL searches help with platform-level troubleshooting and identifying performance issues.

