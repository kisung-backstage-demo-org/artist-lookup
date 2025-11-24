# Artist Lookup Service

[![Build Status](https://github.com/kisung-backstage-demo-org/artist-lookup/workflows/Build/badge.svg)](https://github.com/kisung-backstage-demo-org/artist-lookup/actions)
[![codecov](https://codecov.io/gh/kisung-backstage-demo-org/artist-lookup/branch/main/graph/badge.svg)](https://codecov.io/gh/kisung-backstage-demo-org/artist-lookup)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A comprehensive microservice for searching and retrieving artist information, featuring full Backstage integration with CI/CD, API documentation, TechDocs, and Datadog observability.

## Features

- Fast artist search with Redis caching
- RESTful API with OpenAPI documentation
- Integration with Spotify and MusicBrainz
- Full observability with Datadog
- Automated CI/CD with GitHub Actions
- Comprehensive monitoring and alerting

## Quick Start

```bash
# Clone repository
git clone https://github.com/kisung-backstage-demo-org/artist-lookup.git
cd artist-lookup

# Run with Docker Compose
docker-compose up -d

# Verify
curl http://localhost:8080/actuator/health
```

## API Usage

```bash
# Search for artists
curl "http://localhost:8080/api/v1/artists?q=Beatles"

# Get artist by ID
curl "http://localhost:8080/api/v1/artists/123"
```

## Documentation

Full documentation is available at: [Backstage TechDocs](https://backstage.example.com/docs/default/component/artist-lookup)

- [Getting Started](docs/getting-started.md)
- [Architecture](docs/architecture/overview.md)
- [API Documentation](https://api-docs.example.com/artist-lookup)
- [Monitoring Guide](docs/operations/monitoring.md)

## Monitoring & Observability

This service is fully integrated with **Datadog**:

- **Dashboard**: https://app.datadoghq.com/dashboard/abc-123
- **APM**: https://app.datadoghq.com/apm/service/artist-lookup
- **Logs**: https://app.datadoghq.com/logs?query=service:artist-lookup

## Dependencies

- Java 17
- Spring Boot 3.1
- PostgreSQL 14
- Redis 7
- Docker & Kubernetes

## TODOs

<!-- TODO: Add GraphQL API support -->
<!-- TODO: Implement artist recommendation engine -->
<!-- TODO: Add support for album and track lookup -->
<!-- TODO: Integrate with additional data sources (Apple Music, YouTube) -->
<!-- TODO: Add real-time artist activity tracking -->
<!-- TODO: Implement advanced search with filters (genre, popularity, year) -->
<!-- TODO: Add batch import functionality for artist data -->
<!-- TODO: Create admin dashboard for data management -->

## CI/CD Pipelines

This project uses GitHub Actions for CI/CD:

- **Build & Test**: Runs on every push/PR
- **Deploy**: Manual deployment to staging/production
- **Security Scan**: Weekly security and dependency scanning

## Contributing

Please read [CONTRIBUTING.md](docs/development/contributing.md) for details on our code of conduct and the process for submitting pull requests.

## Support

- **Slack**: #artist-lookup
- **Email**: team-a@example.com
- **PagerDuty**: artist-lookup service

## License

This project is licensed under the Apache License 2.0 - see the LICENSE file for details.

