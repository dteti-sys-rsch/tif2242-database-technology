
# Final Project — Modernize the Sakila DB for a Streaming Service

**Course:** TIF2242 – Database Systems  
**Instructor:** Dr. Guntur D Putra  
**Due Date:** Monday, 30 March 2026 at **07.59** with a presentation during our last class

## Overview
[Sakila](https://github.com/jOOQ/sakila) is a classic sample database originally designed to model a DVD rental store. For your final project, adapt and extend the Sakila schema to design a relational database for a modern streaming service (video-on-demand). Your design must support streaming‑specific features and include analytics-ready structures for business insights.

This is a capstone: combine data modeling, schema migration planning, SQL DDL, and analytics query design.

## Goals
- Map the existing [Sakila schema](https://github.com/jOOQ/sakila) to a streaming domain and justify each change.  
- Add new entities/relationships typical for streaming (user profiles, subscriptions, streaming sessions, episodes, availability windows, content licensing, devices, DRM/licensing metadata, recommendations, watch history, playlists).  
- Design analytics artifacts (aggregated tables, event logs, or schemas suitable for time-series analysis) to support metrics such as plays, session length, retention, churn prediction, and content popularity.  
- Provide SQL DDL for the final schema, sample migration notes, and example analytic queries.
- You will need to setup your `postgres` environment on your own machine to work on and complete this final project. Please refer to [my quick tutorial](../extras/docker-compose-setup.md) on how to setup a Docker-based `postgres` environment.

## Requirements
1. Mapping & Migration Plan (20%):
	- A table-by-table mapping from Sakila to your new schema (what you keep, rename, split, or drop).  
	- For renamed/repurposed tables show notes describing data transformation (e.g., converting `rental` rows into `streaming_session` events) or example ALTER/MIGRATION SQL.  
2. Logical Schema & ERD (20%):
	- Final relational schema (table list with attributes, PKs, FKs, NOT NULL/UNIQUE constraints).  
	- An ERD (Crow's Foot) showing cardinalities and important relationships.  
3. SQL DDL (20%):
	- `CREATE TABLE` statements for all final tables including PKs, FKs, indexes for analytic workloads, and any CHECK constraints.  
4. Analytics Design & Example Queries (20%):
	- At least 6 useful analytics queries (e.g., daily active users, average watch time by content, retention cohort query, top content by region, churn indicator query, recommendation‑ready co‑watch matrix).  
	- If you design summary/aggregate tables or event schemas, include their DDL and an example ETL/aggregation SQL.  
5. Sample Data & Demonstration (10%):
	- Provide sample INSERTs (at least 20 rows spread across key tables) or a small SQL dump that demonstrates your schema and queries.  
6. Write-up & Rationale (10%):
	- A short report (1–2 pages) explaining major design choices, normalization tradeoffs, indexing/partitioning strategy for analytics, and privacy / legal considerations (e.g., data retention, PII minimization).

## Suggested Schema Extensions
You are free to come up with your own ideas for the data analytics purposes. However, you may want to refer to some of these examples below:
- `user_profiles` (multiple profiles per account, parental controls)  
- `subscriptions` (plan, start/end, payment method, status)  
- `devices` (device_id, type, os, last_seen)  
- `streaming_sessions` (session_id, profile_id, content_id, start_ts, end_ts, bitrate, device_id)  
- `content` (movie/series flag), `series`, `episodes` (for episodic content)  
- `content_availability` (region, start_date, end_date, license_id)  
- `content_providers` and `licenses` (rights window, territory)  
- `watch_history` / `play_events` (event-level logs for analytics)  
- `ratings`, `reviews`, `watchlists`, `playlists`  
- `recommendation_metrics` (co_watch counts, item similarity)  
- `ads` and `ad_impressions` (if modelling ad-supported tiers)  
- `transcode_profiles` and `cdn_locations` for delivery metadata

## Example Feature Ideas (pick at least 3 to implement conceptually)
- Personalized recommendations (collaborative filtering signals stored as co-watch counts).  
- Adaptive bitrate tracking and quality-of-experience metrics (store average bitrate per session).  
- Regional licensing windows and geo-restriction enforcement in availability tables.  
- Offline downloads tracking (device-level entitlements and expiry).  
- Retention/cohort analysis tables and churn prediction features (labels + feature store).  
- A/B testing support (experiment_id, variant, exposure events) to evaluate UI changes and content placements.

Students must choose at least three features above and show how the schema supports them (tables, example queries, and an explanation of how data is collected/stored).


## Evaluation Criteria (rubric)
- Mapping correctness and migration clarity: 15 pts  
- Completeness of final logical schema (PK/FK/constraints): 20 pts  
- Quality and correctness of SQL DDL: 15 pts  
- Analytics design & example queries (usefulness and correctness): 25 pts  
- Sample data & demonstration: 10 pts  
- Report clarity, tradeoffs, and privacy considerations: 15 pts

Total: 100 pts

## Submission Instructions
- Package your deliverables into a single PDF containing:
    - mapping table
    - ERD image
    - SQL DDL
    - example queries with results (screenshots or sample output), and
    - the short report.  
- Include any SQL files or sample dumps as supplementary attachments (ZIP).  
- Submit via eLOK by the due date. Include your name and student ID on the first page.

## Optional Deliverables (extra credit)
- A runnable Docker image or Docker Compose service that spins up a PostgreSQL (or MySQL) instance with your schema and sample data, plus a script that runs the example analytics queries (5 extra pts).  
- A short demo notebook (Jupyter/Colab) that connects and visualizes at least one analytic metric (5 extra pts).

## Final Presentation
Some of you will be randomly selected to present your work in our last class on Monday 30 March, during which you give a demo of your final database implementation. Please be aware of the following:
- You will need to present a live demo for this purpose, where you will do some queries to demonstrate your final work.
- You may want to prepare a presentation deck to help you talk through your work. However the deck is not mandatory as you can still use your submission files to help pitch your demo.
- Please be mindful that the presentation is mandatory if you are selected. If you happen to be unprepared, some grade deduction may be imposed.
