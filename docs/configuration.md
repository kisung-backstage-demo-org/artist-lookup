# Configuration

## Environment Variables

### Database Configuration
```bash
DB_HOST=localhost
DB_PORT=5432
DB_NAME=artists
DB_USER=artist_user
DB_PASSWORD=your_password
DB_MAX_POOL_SIZE=10
```

### Redis Configuration
```bash
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_password
REDIS_TTL_SECONDS=3600
```

### External APIs
```bash
# Spotify
SPOTIFY_CLIENT_ID=your_client_id
SPOTIFY_CLIENT_SECRET=your_client_secret
SPOTIFY_BASE_URL=https://api.spotify.com/v1

# MusicBrainz
MUSICBRAINZ_BASE_URL=https://musicbrainz.org/ws/2
MUSICBRAINZ_USER_AGENT=ArtistLookup/1.0
```

### Datadog Configuration
```bash
DD_AGENT_HOST=localhost
DD_TRACE_AGENT_PORT=8126
DD_SERVICE=artist-lookup
DD_ENV=production
DD_VERSION=1.0.0
DD_LOGS_INJECTION=true
DD_PROFILING_ENABLED=true
```

### Application Configuration
```bash
SERVER_PORT=8080
MANAGEMENT_PORT=8081
LOG_LEVEL=INFO
```

## application.yml

```yaml
spring:
  application:
    name: artist-lookup
  
  datasource:
    url: jdbc:postgresql://${DB_HOST}:${DB_PORT}/${DB_NAME}
    username: ${DB_USER}
    password: ${DB_PASSWORD}
    hikari:
      maximum-pool-size: ${DB_MAX_POOL_SIZE:10}
      minimum-idle: 2
      connection-timeout: 30000
  
  redis:
    host: ${REDIS_HOST}
    port: ${REDIS_PORT}
    password: ${REDIS_PASSWORD}
    timeout: 2000ms

server:
  port: ${SERVER_PORT:8080}

management:
  server:
    port: ${MANAGEMENT_PORT:8081}
  endpoints:
    web:
      exposure:
        include: health,metrics,prometheus

logging:
  level:
    root: ${LOG_LEVEL:INFO}
    com.example: DEBUG
  pattern:
    console: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"

# Custom Configuration
artist-lookup:
  cache:
    ttl-seconds: ${REDIS_TTL_SECONDS:3600}
  external-apis:
    spotify:
      base-url: ${SPOTIFY_BASE_URL}
      client-id: ${SPOTIFY_CLIENT_ID}
      client-secret: ${SPOTIFY_CLIENT_SECRET}
    musicbrainz:
      base-url: ${MUSICBRAINZ_BASE_URL}
      user-agent: ${MUSICBRAINZ_USER_AGENT}
```

