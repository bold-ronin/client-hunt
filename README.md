##UPDATE
##client Hunt web scouty.ai
# Kloi Web-VERSION

Kloi Web is the browser-based version of Kloi, built with React, TypeScript, and Vite.  
It shares the same architecture, authentication model, and feature set as the mobile app, adapted for a modern web environment.

The application is powered by Supabase for authentication and database management, and OpenRouter for LLM access.

---

## Overview

Kloi Web delivers a fast, secure, and production-ready web experience with:

- Email authentication (OTP & Magic Link)
- Google OAuth
- Secure email change flow
- User profile management
- Supabase Edge Functions for backend logic
- OpenRouter integration for LLM responses
- Clean and scalable architecture

This repository contains the web implementation only.

---

## Tech Stack

- React
- TypeScript
- Vite
- Supabase
  - Auth
  - PostgreSQL
  - Row Level Security (RLS)
  - Edge Functions
- OpenRouter API (LLMs)

---

## Architecture

The web app mirrors the mobile app architecture.

### Frontend
- React + TypeScript
- Modular feature-based structure
- Auth state listener for automatic routing
- Protected routes
- Reusable UI components

### Backend (Supabase)
- Supabase Auth for user sessions
- `profiles` table for user metadata
- Row Level Security enabled
- Edge Functions for:
  - LLM request handling
  - Secure OpenRouter API calls
  - Server-side logic

### LLM Layer
- OpenRouter API key stored securely in Supabase Edge Functions
- No LLM keys exposed to the frontend
- Requests proxied through Edge Functions

---

## Authentication

### Email Authentication

Web supports both:

- OTP (numeric code)
- Magic Link (browser-friendly)

Template behavior in Supabase determines whether users receive:
- `{{ .Token }}` (OTP)
- `{{ .ConfirmationURL }}` (Magic link)

### Google OAuth

- Native browser OAuth flow
- Session automatically managed by Supabase

---

## Database Schema

### profiles

```sql
create table profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  full_name text,
  avatar_url text,
  created_at timestamp with time zone default now()
);
