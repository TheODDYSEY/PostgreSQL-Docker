# Data Engineering with PostgreSQL

This repository provides resources for practicing data engineering concepts using PostgreSQL. It includes Docker commands to set up and interact with a PostgreSQL database, SQL scripts to create tables, insert sample data, and perform various SQL operations, as well as instructions for getting started.

## Setup PostgreSQL with Docker

To set up PostgreSQL using Docker, follow these steps:

1. Pull the PostgreSQL Docker image:

    ```bash
    docker pull postgres
    ```

2. Run a PostgreSQL container:

    ```bash
    docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres
    ```

3. Create a new database:

    ```bash
    docker exec -u postgres data-engineering-postgres createdb postgres-db
    ```

4. Connect to the PostgreSQL container:

    ```bash
    docker exec -it data-engineering-postgres psql -U postgres -d postgres-db
    ```

5. Use `\dt` to view the tables in the database.

## Database Operations

### Create Database

```sql
CREATE DATABASE db;
```

### Connect to Database

```sql
\c db
```

```markdown
## Database Setup

### Step 1: Create Users Table
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    date_of_birth DATE
);
```

### Step 2: Insert Fake Data into Users Table
```sql
INSERT INTO users (first_name, last_name, email, date_of_birth) VALUES
('John', 'Doe', 'john.doe@example.com', '1990-01-01'),
('Jane', 'Smith', 'jane.smith@example.com', '1992-05-15'),
...
('Grace', 'Wright', 'grace.wright@example.com', '1997-05-10'),
('William', 'Scott', 'william.scott@example.com', '1986-07-22');
```

### Step 3: Create Films Table
```sql
CREATE TABLE films (
    film_id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    release_date DATE,
    price DECIMAL(5,2),
    rating VARCHAR(10),
    user_rating DECIMAL(2,1) CHECK (user_rating >= 1 AND user_rating <= 5)
);
```

### Step 4: Insert Data into Films Table
```sql
INSERT INTO films (title, release_date, price, rating, user_rating) VALUES
('Inception', '2010-07-16', 12.99, 'PG-13', 4.8),
('The Shawshank Redemption', '1994-09-23', 9.99, 'R', 4.9),
...
('La La Land', '2016-12-09', 11.99, 'PG-13', 4.5);
```

### Step 5: Create Film Category Table
```sql
CREATE TABLE film_category (
    category_id SERIAL PRIMARY KEY,
    film_id INTEGER REFERENCES films(film_id),
    category_name VARCHAR(50) NOT NULL
);
```

### Step 6: Insert Data into Film Category Table
```sql
INSERT INTO film_category (film_id, category_name) VALUES
(1, 'Sci-Fi'),
(1, 'Thriller'),
...
(20, 'Music');
```

### Step 7: Create Actors Table
```sql
CREATE TABLE actors (
    actor_id SERIAL PRIMARY KEY,
    actor_name VARCHAR(255) NOT NULL
);
```

### Step 8: Insert Data into Actors Table
```sql
INSERT INTO actors (actor_name) VALUES
('Leonardo DiCaprio'),
('Tim Robbins'),
...
('Emma Stone');
```

### Step 9: Create Film Actors Table
```sql
CREATE TABLE film_actors (
    film_id INTEGER REFERENCES films(film_id),
    actor_id INTEGER REFERENCES actors(actor_id),
    PRIMARY KEY (film_id, actor_id)
);
```

### Step 10: Insert Data into Film Actors Table
```sql
INSERT INTO film_actors (film_id, actor_id) VALUES
(1, 1),
(2, 2),
...
(20, 20);
```
```

## SQL Operations

This section includes various SQL operations such as creating tables, inserting data, performing joins, and using subqueries.

### Inner Join Example

```sql
SELECT f.title, a.actor_name
FROM films f
INNER JOIN film_actors fa ON f.film_id = fa.film_id
INNER JOIN actors a ON fa.actor_id = a.actor_id;
```

### Left Join Example

```sql
SELECT f.title, a.actor_name
FROM films f
LEFT JOIN film_actors fa ON f.film_id = fa.film_id
LEFT JOIN actors a ON fa.actor_id = a.actor_id;
```

### Union Example

```sql
SELECT title AS name
FROM films
UNION
SELECT actor_name AS name
FROM actors
ORDER BY name;
```

### Subquery Example

```sql
SELECT title,
       (SELECT actor_name
        FROM actors a
        JOIN film_actors fa ON a.actor_id = fa.actor_id
        WHERE fa.film_id = f.film_id
        LIMIT 1) AS actor_name
FROM films f;
```

## Conclusion

This repository serves as a practical guide for learning and practicing data engineering concepts using PostgreSQL. You can use Docker to set up a PostgreSQL database and perform various SQL operations to manipulate and query data. Additionally, you can explore different SQL techniques such as joins, subqueries, and unions to analyze and transform data effectively. Happy learning!