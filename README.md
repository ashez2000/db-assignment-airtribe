# Problem Solving Case : bookmyshow

## Tables

```sql
CREATE TABLE theatre (
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE,
    location VARCHAR(100)
);
```

```sql
CREATE TABLE movie (
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL UNIQUE,
    genre VARCHAR(50) NOT NULL,
    duration INT NOT NULL, -- duration of movie in minutes
    language VARCHAR(50) NOT NULL,
    director VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE theatre_show (
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    theatre_id INT NOT NULL,
    movie_id INT NOT NULL,
    date DATE NOT NULL,
    time TIME NOT NULL,

    FOREIGN KEY (theatre_id) REFERENCES theatre(id),
    FOREIGN KEY (movie_id) REFERENCES movie(id)
);
```

## Example entries

```sql
-- theatre entries
INSERT INTO theatre (id, name, location)
VALUES
    (1, 'ABC Cinemas', 'City Center'),
    (2, 'XYZ Theatres', 'Downtown');
```

```sql
-- movie entries
INSERT INTO movie (
    id, title, genre, duration, language, director
)

VALUES
    (1, 'Inception', 'Science Fiction', 148, 'English', 'Christopher Nolan'),
    (2, 'The Shawshank Redemption', 'Drama', 142, 'English', 'Frank Darabont');
```

```sql
-- show entries
INSERT INTO theatre_show (
    id, theatre_id, movie_id, date, time
)

VALUES
(1, 1, 1, '2024-03-25', '13:00'),
(2, 1, 2, '2024-03-25', '15:30'),
(3, 2, 1, '2024-03-25', '14:00'),
(4, 2, 2, '2024-03-26', '17:00');
```

## Queries

Write a query to list down all the shows on a given date at a given theatre along with their respective show timings

```sql
SELECT s.id AS show_id, m.title, s.time
FROM theatre_show s
JOIN movie m ON s.movie_id = m.id
WHERE s.theatre_id = ? AND s.date = ?;
-- ? is placeholder for query parameters
```
