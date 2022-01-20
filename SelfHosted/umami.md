---
title: umami
description: 
published: true
date: 2022-01-20T12:47:11.977Z
tags: 
editor: markdown
dateCreated: 2022-01-20T12:46:57.482Z
---

# Présentation
Umami est une alternative à google analytics. Il permet de récupérer des données d'un site afin de connaître plusieurs informations de son audience. Il est totalement open source et très simple d'utilisation. 
 
# Installation
# Tabs {.tabset}
## Docker-Compose
 
Créer un répertoire où seront stockées les données de umami. Pour ma part je le met dans /srv/docker
```bash
cd /srv/docker
mkdir /srv/docker/umami
```
 
Ensuite créer un fichier 
```bash
touch /srv/docker/umami/schema.postgresql.sql
```
 
Puis éditez le fichier et copier le code ci-dessous
```bash
drop table if exists event;
drop table if exists pageview;
drop table if exists session;
drop table if exists website;
drop table if exists account;
 
create table account (
    user_id serial primary key,
    username varchar(255) unique not null,
    password varchar(60) not null,
    is_admin bool not null default false,
    created_at timestamp with time zone default current_timestamp,
    updated_at timestamp with time zone default current_timestamp
);
 
create table website (
    website_id serial primary key,
    website_uuid uuid unique not null,
    user_id int not null references account(user_id) on delete cascade,
    name varchar(100) not null,
    domain varchar(500),
    share_id varchar(64) unique,
    created_at timestamp with time zone default current_timestamp
);
 
create table session (
    session_id serial primary key,
    session_uuid uuid unique not null,
    website_id int not null references website(website_id) on delete cascade,
    created_at timestamp with time zone default current_timestamp,
    hostname varchar(100),
    browser varchar(20),
    os varchar(20),
    device varchar(20),
    screen varchar(11),
    language varchar(35),
    country char(2)
);
 
create table pageview (
    view_id serial primary key,
    website_id int not null references website(website_id) on delete cascade,
    session_id int not null references session(session_id) on delete cascade,
    created_at timestamp with time zone default current_timestamp,
    url varchar(500) not null,
    referrer varchar(500)
);
 
create table event (
    event_id serial primary key,
    website_id int not null references website(website_id) on delete cascade,
    session_id int not null references session(session_id) on delete cascade,
    created_at timestamp with time zone default current_timestamp,
    url varchar(500) not null,
    event_type varchar(50) not null,
    event_value varchar(50) not null
);
 
create index website_user_id_idx on website(user_id);
 
create index session_created_at_idx on session(created_at);
create index session_website_id_idx on session(website_id);
 
create index pageview_created_at_idx on pageview(created_at);
create index pageview_website_id_idx on pageview(website_id);
create index pageview_session_id_idx on pageview(session_id);
create index pageview_website_id_created_at_idx on pageview(website_id, created_at);
create index pageview_website_id_session_id_created_at_idx on pageview(website_id, session_id, created_at);
 
create index event_created_at_idx on event(created_at);
create index event_website_id_idx on event(website_id);
create index event_session_id_idx on event(session_id);
 
insert into account (username, password, is_admin) values ('admin', '$2b$10$BUli0c.muyCW1ErNJc3jL.vFRFtFJWrT8/GcR4A.sUdCznaXiqFXa', true);
```
 
Enfin vous pouvez lancer une stack docker :
 
```yaml
version: '3'
services:
  umami:
    image: ghcr.io/mikecao/umami:postgresql-latest
    ports:
      - "3010:3000"
    environment:
      DATABASE_URL: postgresql://umami:umami@db:5432/umami
      DATABASE_TYPE: postgresql
      HASH_SALT: H6ei6O1tdLNxIQLRs4Mw
    depends_on:
      - db
    restart: always
  db:
    image: postgres:12-alpine
    environment:
      POSTGRES_DB: umami
      POSTGRES_USER: umami
      POSTGRES_PASSWORD: umami
    volumes:
      - /srv/docker/umami/schema.postgresql.sql:/docker-entrypoint-initdb.d/schema.postgresql.sql:ro
      - /srv/docker/umami/db:/var/lib/postgresql/data
    restart: always
volumes:
  umami-db-data:
```
 
> L'utilisateur par défaut est **admin** et mot de passe est **umami** 
{.is-info}
 
> Umami sera accessible à l'adresse **http://votre_ip:3010**
{.is-success}
 
# Configuration
## Ajoutez un site
Allez dans Settings, puis cliquez sur "Add Website"
 
renseignez le nom DNS du site en question. Il vous faudra ensuite copier le code de trackage entre les balises `<head>` `</head>` de votre site.