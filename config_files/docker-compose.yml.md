```yml
version: '3.8'
services:
  database:
    image: postgres:14
    environment:
        POSTGRES_USER: '${DB_USER}'
        POSTGRES_PASSWORD: '${DB_PASSWORD}'
        POSTGRES_DB: '${DB_NAME}'
    ports:
        - '5432:5432'
    healthcheck:
        test: ['CMD-SHELL', 'pg_isready -U postgres']
        interval: 10s
        timeout: 5s
        retries: 5
  api:
    build: .
    ports:
        - '3000:3000'
    environment:
        API_HOST: '${API_HOST}'
        API_PORT: '${API_PORT}'
        API_PREFIX: '${API_PREFIX}'
        # DATABASE
        DB_HOST: '${DB_HOST}'
        DB_PORT: '${DB_PORT}'
        DB_NAME: '${DB_NAME}'
        DB_USER: '${DB_USER}'
        DB_PASSWORD: '${DB_PASSWORD}'
    depends_on:
        - database
```