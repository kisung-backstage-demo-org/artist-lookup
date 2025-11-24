# Monitoring & Observability

The Artist Lookup Service is fully integrated with Datadog for comprehensive monitoring and observability.

## Datadog Integration

### Key Dashboards

#### Service Overview Dashboard
**URL**: https://app.datadoghq.com/dashboard/abc-123

This dashboard shows:
- Request rate (requests/sec)
- Response time (p50, p95, p99)
- Error rate (%)
- Service uptime

#### APM Dashboard
**URL**: https://app.datadoghq.com/apm/service/artist-lookup

- Distributed traces
- Service map
- Performance bottlenecks
- Database query performance

#### Infrastructure Dashboard
- CPU usage
- Memory usage
- JVM heap metrics
- GC activity

### Logs

All logs are sent to Datadog with structured JSON format.

**Search logs**: https://app.datadoghq.com/logs?query=service:artist-lookup

Common log queries:
```
# Error logs
service:artist-lookup status:error

# Slow requests (>1s)
service:artist-lookup @duration:>1000

# Database errors
service:artist-lookup @db.error:*

# Cache misses
service:artist-lookup @cache.hit:false
```

### Metrics

Key metrics tracked:

#### Application Metrics
- `artist_lookup.requests.count` - Total requests
- `artist_lookup.requests.duration` - Request duration
- `artist_lookup.cache.hit_ratio` - Cache hit ratio
- `artist_lookup.external_api.calls` - External API calls

#### System Metrics
- `jvm.memory.used` - JVM memory usage
- `jvm.gc.pause` - GC pause time
- `system.cpu.usage` - CPU usage
- `system.disk.usage` - Disk usage

#### Database Metrics
- `postgresql.connections.active` - Active connections
- `postgresql.queries.duration` - Query duration
- `postgresql.deadlocks` - Deadlock count

### APM & Tracing

Every request is traced with:
- Request ID (correlation)
- User ID
- Source service
- Downstream services
- Database queries
- Cache operations
- External API calls

**View traces**: https://app.datadoghq.com/apm/traces?query=service:artist-lookup

### Alerts

#### Critical Alerts (PagerDuty)
- ❗ Error rate > 1% for 5 minutes
- ❗ p99 latency > 1s for 5 minutes
- ❗ Service unavailable (health check fails)
- ❗ Database connection pool exhausted

#### Warning Alerts (Slack)
- ⚠️ Error rate > 0.5% for 10 minutes
- ⚠️ Cache hit ratio < 80% for 15 minutes
- ⚠️ High memory usage (>85%)
- ⚠️ Slow database queries (>500ms)

#### Info Alerts (Email)
- ℹ️ Deployment completed
- ℹ️ Configuration changed
- ℹ️ Scale-up/down events

### SLIs & SLOs

| Metric | SLI | SLO | Current |
|--------|-----|-----|---------|
| Availability | Successful requests / Total requests | 99.9% | 99.95% |
| Latency | p99 < 500ms | 99% | 99.2% |
| Error Rate | Errors / Total requests | < 0.1% | 0.05% |

### Synthetic Monitoring

Datadog Synthetic tests run every 5 minutes:

1. **API Health Check**
   - Endpoint: `/actuator/health`
   - Expected: 200 OK

2. **Artist Search**
   - Endpoint: `/api/v1/artists?q=Beatles`
   - Expected: 200 OK, response time < 200ms

3. **Database Connectivity**
   - Endpoint: `/api/v1/artists/test-id`
   - Expected: 200 or 404, no 5xx errors

### Custom Metrics

You can add custom metrics using the Datadog StatsD client:

```java
import com.timgroup.statsd.StatsDClient;

// Increment counter
statsd.incrementCounter("artist_lookup.search.count");

// Record timing
statsd.recordExecutionTime("artist_lookup.search.duration", duration);

// Set gauge
statsd.recordGaugeValue("artist_lookup.cache.size", cacheSize);
```

### Profiling

Continuous profiling is enabled to identify performance bottlenecks:

**View profiles**: https://app.datadoghq.com/profiling/search?query=service:artist-lookup

## Grafana (Optional)

Alternative dashboards available in Grafana:
- https://grafana.example.com/d/artist-lookup

## Runbook

For troubleshooting guides, see:
- [Troubleshooting Guide](troubleshooting.md)
- [Runbook](https://wiki.example.com/runbooks/artist-lookup)

