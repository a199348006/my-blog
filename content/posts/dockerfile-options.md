---
title: "Dockerfile Options"
date: 2022-03-30T15:36:30+08:00
draft: false
tags: ["Docker"]
categories: ["Docker"]
description: "Dockerfile and docker-compose.yml使用到的參數配置。"
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 練習建立Dockerfile and docker-compose.yml

## Dockerfile sample

```docker
# Base image
FROM node:16.13.2-alpine
# Create app directory
WORKDIR /usr/api
# Install app dependencies
COPY package.json .
RUN npm install
# Bundle app source
COPY . .
EXPOSE 6789
CMD [ "npm", "start" ]
```

## docker-compose.yml sample

```yml
version: "3.8"

services:
  node:
    image: node:16.13.2-alpine
    build: . # build from Dockerfile
    container_name: node-api # change default container name
    depends_on: # build after depends_on items
      - db
    restart: unless-stopped
    env_file: ./.env 
    environment:
      DB: $DB
      DB_USER: $DB_USER
      DB_PASSWORD: $DB_PASSWORD
      DB_HOST: db
      DB_PORT: $DB_PORT
    ports:
      - "6789:6789" # localhost:container
    networks:
      - backend
  db:
    image: postgres:alpine
    container_name: db-postgres
    restart: unless-stopped
    env_file: ./.env
    environment:
      POSTGRES_DB: $DB
      POSTGRES_USER: $DB_USER
      POSTGRES_PASSWORD: $DB_PASSWORD
    ports:
      - "5432:5432"
    networks:
      - backend

networks:
  backend:
```

## Accidents

_**使用depend_on，node-api在資料庫還沒執行時先啟動造成db connect error**_

## 參考來源

[Docker Compose](https://www.runoob.com/docker/docker-compose.html)
