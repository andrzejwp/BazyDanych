# Prepare the database

To import the Sakila database into the server use the following command:

```
mysql --host=localhost --port=3306 --protocol=tcp -u root -p < sakila-schema.sql
mysql --host=localhost --port=3306 --protocol=tcp -u root -p < sakila-data.sql
```

# Explore the Sakila DB

Using the ``mysql`` shell or the script view in MySQL Workbench type in the following commands to gain some orientation in the database. Consult the ER diagram (in Workbench or on the Sakila website https://dev.mysql.com/doc/sakila/en/sakila-structure.html).

```
show databases;
```
```
use sakila
```
```
show tables
```
```
SELECT * FROM actor LIMIT 1 \G;
```

# Explore the relations

Find the actor whose ID in the database is 10:

```
SELECT * FROM actor WHERE actor_id=10;
```

Hint: the ``\G`` or ``;`` at the end of the SQL command determine how the result will be displayed. ``\G`` is useful for wide tables (with many columns).

Now find the films, where actor with ID=10 is starring:

```
SELECT * FROM film_actor where actor_id=10;
```

Write down the IDs of the films (from ``film_id`` column) and get the titles of those films after putting them in the ```IN()``` clause:

```
SELECT film_id,title FROM film where film_id IN (FOUND_ID1, FOUND_ID2, ...)
```

# Joining data from several tables

The procedure you used above to elicit the information about films starring actor ID=10 is cumbersome and inefficient. The proper way to do this is using a construct called *joins*. It will let us display the complete information using one SQL query. We'll rewrite the previous command using a join, but let's start with something simpler and explore the ``1:n`` relation between ``film`` and ``language``.

```
SELECT film.film_id, film.title, language.name FROM film INNER JOIN language ON (film.language_id=language.language_id) LIMIT 10;
```

Now, let's try to display the same for a ``n:n`` relation, like the one between ``film`` and ``category``.

```
SELECT film.title, category.name FROM film INNER JOIN film_category ON (film.film_id =film_category.film_id) INNER JOIN category ON (film_category.category_id=category.category_id) LIMIT 10;
```

Now try yourself - display how many films there are, per category (hint: use ``GROUP BY`` and ``count(*)``).


# SQL Language practice

Using Sakila database :

1. Write a query that will select names of 10 top starring actors (those who cast in the
highest number of movies)
1. Write a query that will select movie categories having more than 10 films in the DB
1. Write a query that will tell us which months have the most rentals (use ``payment`` table)
1. Write a query that will tell us what this the average price of rental
1. Check which movies are the most rented ones (top 10)
1. Determine the prices of the most frequently rented movies
