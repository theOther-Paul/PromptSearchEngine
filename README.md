# PromptSearchEngine
A search engine like web app that will be used to search through AI prompts submitted by users

## Architecture

- Frontend: Flask
- Backend API: Flask, SQLAlchemy ORM
- Database: PostgreSQL

### Goals

- Allow users to create, read, update, delete prompts.
- Support public/private/unlisted visibility.
- Fast search with relevance (full-text + tag filters).
- Track usage analytics (counts, last_used).
- Simple, secure REST API backend (Flask + Python).

### Features

- Prompt creation and management
- Search functionality with full-text and tag filters
- Usage analytics tracking
- Add LLM capabilities for reccomending prompts

## System architecture
- Components:
- Frontend: SPA (React / Svelte / Vue) served from static hosting (Netlify / AWS S3+CloudFront) or via Flask templates for simple MVP.
- Backend API: Flask app (Blueprints), SQLAlchemy ORM, Alembic migrations.
- Database: PostgreSQL (managed or self-hosted). Use pgcrypto or UUID extension.
- Cache: Redis for rate-limiting and short-term caching.
- Object storage: S3-compatible for attachments.
- Reverse proxy / TLS: Nginx or managed platform.
- Data flow:  - Client -> HTTPS -> Flask API -> PostgreSQL (CRUD) + Redis for ephemeral data -> return results.

## Authentication and authorization
- Options:
  - Local auth with bcrypt/argon2 hashed passwords and email verification.
  - OAuth 2.0 / OIDC (Google, GitHub) for faster onboarding.
- Authorization rules:
  - Prompt owner or admin can edit/delete private prompts.
  - Public prompts readable by anyone.
  - Unlisted prompts readable by direct link or owner.
- Token handling:
  - Issue JWTs with short TTL for API; refresh tokens stored server-side (optional).
  - Blacklist revoked refresh tokens.
