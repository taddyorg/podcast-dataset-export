# Taddy API Podcast Dataset Sample

This is a sample of the Taddy API Podcast Dataset. It contains 14929 podcasts and 10544 episodes. The full dataset contains 4+ million podcasts and 130+ million episodes. If you want to purchase the full dataset, please contact [danny@taddy.org](mailto:danny@taddy.org).

## Data Format

The data is in Parquet format. There are libraries for reading Parquet files in most programming languages.

## Table Definitions

Podcast Series Table

```sql
CREATE TABLE podcastseries (
    id BIGSERIAL,
    uuid uuid PRIMARY KEY,
    created_at timestamp with time zone NOT NULL DEFAULT now(),
    updated_at timestamp with time zone,
    source character varying(255),
    hash character varying(255) UNIQUE,
    hash_timestamp bigint,
    genres_hash character varying(255),
    itunes_info_hash character varying(255),
    date_published timestamp with time zone,
    name character varying(255),
    description text,
    image_url text,
    itunes_id bigint UNIQUE,
    series_type character varying(255),
    copyright text,
    country_of_origin character varying(255),
    language character varying(255),
    website_url text,
    author_name character varying(255),
    content_type character varying(255),
    rss_url text UNIQUE,
    rss_owner_name character varying(255),
    rss_owner_public_email text,
    is_explicit_content boolean,
    is_completed boolean,
    is_blocked boolean,
    children_hash character varying(255)
);
```

Podcast Episode Table

```sql
CREATE TABLE podcastepisode (
    id BIGSERIAL,
    uuid uuid PRIMARY KEY,
    created_at timestamp with time zone NOT NULL DEFAULT now(),
    updated_at timestamp with time zone,
    hash character varying(255),
    hash_timestamp bigint,
    date_published timestamp with time zone,
    name character varying(255),
    description text,
    image_url text,
    series_uuid uuid NOT NULL,
    guid text NOT NULL,
    series_uuid_plus_guid text NOT NULL UNIQUE,
    subtitle text,
    audio_url text,
    video_url text,
    file_length integer,
    file_type character varying(255),
    duration integer,
    season_number integer,
    episode_number integer,
    episode_type character varying(255),
    website_url text,
    is_explicit_content boolean,
    is_removed boolean,
    series_hash character varying(255),
    is_blocked boolean
);
```