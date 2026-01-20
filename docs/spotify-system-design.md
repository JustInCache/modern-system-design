# Spotify – High‑Level System Design Architecture

## 1. Goals & Requirements

### Functional Requirements
- User authentication & profile management
- Music search (songs, artists, albums, playlists)
- Music streaming (low latency, high availability)
- Playlist creation & management
- Recommendations & personalization
- Likes, follows, downloads (offline)

### Non‑Functional Requirements
- Massive scalability (100M+ users)
- Low latency streaming
- High availability & fault tolerance
- Global distribution
- Data consistency (eventual for most, strong for auth/payments)
- Cost‑efficient storage & delivery

---

## 2. High‑Level Architecture Overview

```
Client (Mobile/Web/Desktop)
        |
   API Gateway
        |
-----------------------------
|        Backend Services    |
-----------------------------
| Auth | User | Music | Play |
| Meta | Search | Reco | Ads |
-----------------------------
        |
-----------------------------
|   Data Layer & Caching     |
-----------------------------
        |
-----------------------------
| CDN + Media Storage        |
-----------------------------
```

---

## 3. Client Layer

### Platforms
- iOS / Android apps
- Web player
- Desktop apps

### Responsibilities
- User interaction & UI
- Adaptive bitrate streaming
- Local caching for offline playback
- Telemetry & analytics events

---

## 4. API Gateway

### Responsibilities
- Single entry point for all clients
- Authentication & authorization (JWT / OAuth)
- Rate limiting & request validation
- Routing requests to internal services

Examples:
- `/login`
- `/search?q=...`
- `/playlist/{id}`

---

## 5. Core Backend Services (Microservices)

### 5.1 Authentication Service
- User login / signup
- Token generation & validation
- Integrates with payment & subscription service

### 5.2 User Service
- User profiles
- Preferences (language, device, playback settings)

### 5.3 Music Metadata Service
- Song, album, artist metadata
- Duration, genre, rights info

### 5.4 Playlist Service
- Create/update/delete playlists
- Collaborative playlists

### 5.5 Search Service
- Full‑text search (songs, artists, playlists)
- Powered by Elasticsearch / OpenSearch

### 5.6 Recommendation Service
- Personalized playlists (Discover Weekly)
- Uses ML models
- Inputs: listening history, likes, skips

### 5.7 Streaming Control Service
- Validates access rights
- Provides signed URLs for audio chunks

### 5.8 Ads Service (Free Tier)
- Ad targeting
- Ad insertion logic

---

## 6. Data Storage Layer

### Relational Databases (Strong Consistency)
- User accounts
- Subscriptions & payments

Examples: PostgreSQL / MySQL

### NoSQL Databases (Scalable)
- User activity
- Playlists
- Listening history

Examples: Cassandra / DynamoDB

### Search Index
- Songs, artists, playlists

Example: Elasticsearch

---

## 7. Caching Layer

### Purpose
- Reduce database load
- Improve latency

### Technologies
- Redis / Memcached

### Cached Data
- User sessions
- Frequently accessed playlists
- Trending songs

---

## 8. Media Storage & Streaming

### Audio Storage
- Object storage (S3 / GCS)
- Audio split into chunks

### CDN (Critical Component)
- Global content delivery
- Edge caching near users

Flow:
```
Client → CDN → Audio Chunk
```

---

## 9. Recommendation & ML Pipeline

### Data Sources
- Listening events
- Likes, skips, repeats

### Processing
- Event ingestion via Kafka
- Batch processing (Spark)
- Real‑time features (Flink)

### Output
- Personalized playlists
- Song similarity graphs

---

## 10. Analytics & Monitoring

### Event Streaming
- Kafka / Kinesis

### Metrics & Logs
- Latency
- Playback failures
- User engagement

Tools:
- Prometheus
- Grafana
- ELK Stack

---

## 11. Scalability & Reliability

- Horizontal scaling of services
- Load balancers
- Circuit breakers
- Multi‑region deployment
- Blue‑green & canary releases

---

## 12. Security

- HTTPS everywhere
- Encrypted audio URLs
- DRM for content protection
- Role‑based access control

---

## 13. Summary (One‑Line View)

Spotify uses **microservices + CDN‑based streaming + ML‑driven recommendations**, optimized for **low latency, massive scale, and personalization**.

