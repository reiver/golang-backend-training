## 7. Database

### 7.1. Install the Postgres Database Server

### 7.2. Create a Database

Use the Postgres command line tool `psql` to create a new database.

### 7.3. Create a Table

Use the Postgres command line tool `psql` to create a new table (in the database you previously created).

Your table should include a field that is its _primary key_:
```
id BIGSERIAL PRIMARY KEY,
```

And it should include a field named `when_created`:
```sql
when_created TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now(),
```

Of course, you should have other fields besides this one. Make up some type of table. And include fields that make sense for your made up table.

### 7.4. INSERT

Use the Postgres command line tool `psql` to INSERT some new values (into the new table you created in the new database you previously created).

-----

[RETURN](../../README.md)
