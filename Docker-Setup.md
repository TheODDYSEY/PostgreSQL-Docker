## Setting Up PostgreSQL Database for Data Engineering

In this tutorial, we'll guide you through the process of setting up a PostgreSQL database using Docker for your data engineering projects.

### Step 1: Pull PostgreSQL Docker Image
First, pull the PostgreSQL Docker image from the official Docker Hub repository:
```bash
docker pull postgres
```

### Step 2: Run PostgreSQL Container
Now, run a PostgreSQL container with the following command:
```bash
docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres
```
This command creates a PostgreSQL container named "data-engineering-postgres" with the specified password "secret".

### Step 3: Create a Database
Next, create a database inside the PostgreSQL container. Execute the following command:
```bash
docker exec -u postgres data-engineering-postgres createdb postgres-db
```
This command creates a new database named "postgres-db".

### Step 4: Access the Database
To access the PostgreSQL database, use the following command to connect to the container's PostgreSQL shell:
```bash
docker exec -it data-engineering-postgres psql -U postgres -d postgres-db
```
You will be prompted to enter the password you set earlier ("secret"). Once authenticated, you will have access to the PostgreSQL shell.

### Step 5: View Database Tables
To view the tables in the database, use the command:
```sql
\dt
```

```
| Schema |     Name      | Type  |  Owner   |
|--------|---------------|-------|----------|
| public | actors        | table | postgres |
| public | film_actors   | table | postgres |
| public | film_category | table | postgres |
| public | films         | table | postgres |
| public | users         | table | postgres |
```

This command displays a list of all tables in the connected database.

### Conclusion
You've now set up a PostgreSQL database using Docker for your data engineering projects. You can start building your data pipelines and performing various data engineering tasks using PostgreSQL.
```
```


