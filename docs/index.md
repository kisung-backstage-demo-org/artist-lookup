# Artist Lookup Service

Welcome to the **Artist Lookup Service** documentation! This is a comprehensive demo microservice showcasing all Backstage features.

## Overview

The Artist Lookup Service is a RESTful API that provides artist information from multiple data sources including Spotify and MusicBrainz.

## Key Features

- 🔍 **Fast Search**: Sub-millisecond artist search with Redis caching
- 📊 **Rich Data**: Aggregated data from multiple sources
- 🔒 **Secure**: OAuth2 authentication and rate limiting
- 📈 **Observable**: Full Datadog integration for monitoring and alerting
- 🚀 **High Performance**: Handles 10k+ requests per second

## Architecture

```
┌─────────────┐
│   Client    │
└──────┬──────┘
       │
       ▼
┌─────────────┐      ┌─────────────┐
│   API GW    │─────▶│   Redis     │
└──────┬──────┘      └─────────────┘
       │
       ▼
┌─────────────┐      ┌─────────────┐
│  Artist API │─────▶│  PostgreSQL │
└──────┬──────┘      └─────────────┘
       │
       ▼
┌─────────────────────────┐
│  External APIs          │
│  - Spotify              │
│  - MusicBrainz          │
└─────────────────────────┘
```

## Quick Links

- [API Documentation](https://api-docs.example.com/artist-lookup)
- [Datadog Dashboard](https://app.datadoghq.com/dashboard/abc-123)
- [GitHub Repository](https://github.com/kisung-backstage-demo-org/artist-lookup)
- [Runbook](https://wiki.example.com/runbooks/artist-lookup)

## Monitoring & Observability

This service is fully integrated with **Datadog** for comprehensive observability:

### Metrics
- Request rate, latency, and error rates
- Cache hit/miss ratios
- Database connection pool metrics
- JVM memory and GC metrics

### Logs
- Structured JSON logging
- Correlation IDs for distributed tracing
- Log levels: DEBUG, INFO, WARN, ERROR

### APM & Tracing
- Distributed tracing across all services
- Performance profiling
- Database query analysis

### Alerts
- High error rate (>1%)
- High latency (p99 > 500ms)
- Low cache hit ratio (<80%)
- Database connection issues

## Dependencies

| Service | Purpose | SLA |
|---------|---------|-----|
| PostgreSQL | Primary data store | 99.99% |
| Redis | Caching layer | 99.9% |
| Spotify API | Artist metadata | 99.5% |
| MusicBrainz API | Artist metadata | 99.0% |

## TODOs

<!-- TODO: Add GraphQL API support -->
<!-- TODO: Implement artist recommendation engine -->
<!-- TODO: Add support for album and track lookup -->
<!-- TODO: Integrate with additional data sources -->
<!-- TODO: Add real-time artist activity tracking -->

## Support

For issues or questions:
- Slack: #artist-lookup
- Email: team-a@example.com
- PagerDuty: artist-lookup service

