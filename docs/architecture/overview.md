# Architecture Overview

## System Architecture

The Artist Lookup Service follows a microservices architecture with the following components:

```
                    ┌──────────────┐
                    │   Internet   │
                    └───────┬──────┘
                            │
                    ┌───────▼──────┐
                    │   AWS ALB    │
                    └───────┬──────┘
                            │
                ┌───────────┴───────────┐
                │                       │
        ┌───────▼──────┐       ┌───────▼──────┐
        │ API Gateway  │       │ API Gateway  │
        │  (Primary)   │       │  (Secondary) │
        └───────┬──────┘       └───────┬──────┘
                │                       │
                └───────────┬───────────┘
                            │
                    ┌───────▼──────┐
                    │   Service    │
                    │   Mesh       │
                    └───────┬──────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼──────┐    ┌───────▼──────┐    ┌──────▼──────┐
│   Artist     │    │   Cache      │    │  External   │
│   Service    │◄───│   Layer      │    │    APIs     │
│   (Java)     │    │   (Redis)    │    │             │
└───────┬──────┘    └──────────────┘    └─────────────┘
        │
┌───────▼──────┐
│  PostgreSQL  │
│   Database   │
└──────────────┘
```

## Components

### API Layer
- **Spring Boot** application
- RESTful endpoints
- OpenAPI 3.0 specification
- JWT authentication
- Rate limiting

### Caching Layer
- **Redis** for high-speed caching
- TTL-based expiration
- Cache-aside pattern
- 90%+ hit ratio target

### Data Layer
- **PostgreSQL** primary database
- Read replicas for scalability
- Connection pooling (HikariCP)
- Flyway migrations

### External Integrations
- **Spotify API**: Artist metadata
- **MusicBrainz API**: Artist information
- Circuit breaker pattern (Resilience4j)

## Design Principles

### 1. High Availability
- Multi-AZ deployment
- Auto-scaling (2-10 instances)
- Health checks and self-healing
- 99.9% uptime SLA

### 2. Performance
- Sub-100ms p99 latency
- 10k+ requests/second capacity
- Efficient database indexing
- Aggressive caching

### 3. Observability
- Datadog APM integration
- Structured logging
- Distributed tracing
- Real-time metrics

### 4. Security
- OAuth2/JWT authentication
- API rate limiting
- Input validation
- SQL injection prevention
- Secrets management (AWS Secrets Manager)

## Technology Stack

- **Language**: Java 17
- **Framework**: Spring Boot 3.1
- **Database**: PostgreSQL 14
- **Cache**: Redis 7
- **Build**: Maven
- **Container**: Docker
- **Orchestration**: Kubernetes
- **CI/CD**: GitHub Actions
- **Monitoring**: Datadog
- **Cloud**: AWS (EKS, RDS, ElastiCache)

