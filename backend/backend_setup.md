# Backend Architecture Overview

This document provides a high-level summary of the major backend components implemented in SlugSync.  
While the core backend code is private, this overview explains how the system is structured and how responsibilities are separated.

---

## 1. Application & Environment Setup
- Loads environment variables (`.env`)
- Initializes FastAPI application entrypoint
- Configures SQLModel database engine for persistence

---

## 2. Security & JWT Configuration
- Core authentication parameters:
  - secret key
  - hashing algorithm
  - token expiration rules
- OAuth2 token handler for bearer authentication

---

## 3. Authentication Data Models
- Shared models used during authentication flows:
  - JWT access tokens
  - token payload structure
  - Google OAuth request payload

---

## 4. User Data Models & Database Schema
- SQLModel schema for users
- Pydantic models for creation and response
- Stores host permissions and account metadata

---

## 5. Event Data Models & Validation
- SQLModel schema for events
- Input/output validation models
- Time-based validation to ensure consistent event scheduling

---

## 6. Database Initialization & Session Management
- Automatic table creation on startup
- Database session dependency injection for request handling

---

## 7. Authentication Utility Functions
- JWT creation + expiration handling
- UCSC domain validation
- Internal helpers for token verification and refresh (`/auth/google`)

---

## 8. Authentication Dependencies (Access Control)
- Dependency-based authorization:
  - decode token → resolve user
  - enforce host role for event management
  - enforce admin role for permission approvals

---

## 9. Authentication Endpoints (Google Sign-In)
- Accepts Google ID token from iOS app
- Validates token audience & issuer
- Creates a local user on first sign-in
- Returns SlugSync access token for backend usage

---

## 10. User Management Endpoints
- Retrieve current authenticated user profile
- Admin routes to approve or revoke event-host privileges

---

## 11. Event CRUD Endpoints (Role-Aware)
- Create, read, update, delete events
- Event creation requires host privileges
- Update/delete restricted to event owners
- Query filtering supports tags, search, and dates

---

## 12. Operational & Diagnostic Endpoints
- Health check (`/`) for availability monitoring
- Debug route exposing resolved authentication state during development

---
