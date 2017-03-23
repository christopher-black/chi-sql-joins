# SQL JOINS & AGGREGATES

### JOINS
```SQL
-- Create our tables
CREATE TABLE "user" (
  id SERIAL PRIMARY KEY,
  name VARCHAR(25)
);

INSERT INTO "user" (name)
VALUES ('Chris'), ('Logan'),
('Bri'), ('Lisa'), ('Teigen');

-- SELECT column_name FROM table_name
SELECT "id","name" FROM "user";

CREATE TABLE "hobby" (
  id SERIAL PRIMARY KEY,
  description VARCHAR(100)
);

INSERT INTO "hobby" ("description")
VALUES ('Kayaking'), ('Pottery'),
('Biking'), ('Cooking'), ('Swing Dancing');

SELECT * FROM "hobby";

CREATE TABLE "user_hobby" (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES "user",
  hobby_id INT REFERENCES "hobby",
  skill INT
);

INSERT INTO "user_hobby" ("user_id", "hobby_id", "skill") VALUES (5, 2, 3), (5, 3, 2), (5, 5, 5),
(4, 4, 2), (4, 5, 2), (2, 3, 1), (2, 1, 3),
(3, 2, 2), (3, 1, 1), (3, 4, 3), (1, 1, 2);

-- Alias id as user_id
SELECT "id" as "user_id" FROM "user_hobby";

SELECT * FROM "user" JOIN "user_hobby" ON
"user"."id" = "user_hobby"."user_id";

-- SELECT all data joined together
SELECT * FROM "user"
JOIN "user_hobby" ON "user"."id"="user_hobby"."user_id"
JOIN "hobby" ON "hobby"."id" = "user_hobby"."hobby_id";

-- SELECT hobbies for a specific user (user_id = 3)
SELECT "hobby"."description", "user_hobby"."skill"
FROM "hobby" JOIN "user_hobby"
ON "hobby"."id" = "user_hobby"."hobby_id"
WHERE "user_hobby"."user_id" = 3;
```

### AGGREGATES

```SQL
-- Aggregates
SELECT count(*) FROM "user";

-- Minimum value for skill
SELECT MIN("skill") FROM "user_hobby";

-- Maximum value for skill
SELECT MAX("skill") FROM "user_hobby";

SELECT AVG("skill") FROM "user_hobby";

SELECT SUM("skill") FROM "user_hobby";

SELECT MIN("skill"), MAX("skill") FROM "user_hobby";

SELECT "hobby"."description", count("user_hobby"."hobby_id") FROM "hobby"
JOIN "user_hobby"
ON "hobby"."id" = "user_hobby"."hobby_id"
GROUP BY "hobby"."description";
```
