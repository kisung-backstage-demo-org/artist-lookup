# Getting Started

This guide will help you get started with the Artist Lookup Service.

## Prerequisites

- Java 17+
- Maven 3.8+
- PostgreSQL 14+
- Redis 6+
- Docker (optional)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/kisung-backstage-demo-org/artist-lookup.git
cd artist-lookup
```

### 2. Configure Environment

Create a `.env` file:

```bash
# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=artists
DB_USER=artist_user
DB_PASSWORD=your_password

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# External APIs
SPOTIFY_CLIENT_ID=your_client_id
SPOTIFY_CLIENT_SECRET=your_client_secret
MUSICBRAINZ_USER_AGENT=ArtistLookup/1.0

# Datadog
DD_AGENT_HOST=localhost
DD_TRACE_AGENT_PORT=8126
DD_SERVICE=artist-lookup
DD_ENV=development
```

### 3. Setup Database

```bash
# Create database
psql -U postgres -c "CREATE DATABASE artists;"

# Run migrations
mvn flyway:migrate
```

### 4. Build & Run

```bash
# Build
mvn clean package

# Run
java -jar target/artist-lookup-1.0.0.jar
```

The service will be available at `http://localhost:8080`

## Docker Setup

```bash
# Build image
docker build -t artist-lookup:latest .

# Run with docker-compose
docker-compose up -d
```

## Verify Installation

```bash
# Health check
curl http://localhost:8080/actuator/health

# Search for an artist
curl "http://localhost:8080/api/v1/artists?q=Beatles"
```

## Next Steps

- [Configuration Guide](configuration.md)
- [API Documentation](../architecture/api-design.md)
- [Deployment Guide](../operations/deployment.md)

