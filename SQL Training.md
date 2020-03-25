# SQL Basics
﻿
## Create a table and inert new entries

```sql
CREATE TABLE groceries
	(id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER, aisle INTEGER);
```
```sql
INSERT INTO groceries VALUES (1, "Bananas", 4, 7);
INSERT INTO groceries VALUES(2, "Peanut Butter", 1, 2);
INSERT INTO groceries VALUES(3, "Dark Chocolate Bars", 2, 2);
INSERT INTO groceries VALUES(4, "Ice cream", 1, 12);
INSERT INTO groceries VALUES(5, "Cherries", 6, 2);
INSERT INTO groceries VALUES(6, "Chocolate syrup", 1, 4);
```

## Query a Table
```sql
SELECT * FROM groceries 
```

With sorting
```sql
/* ORDER BY */

SELECT *
FROM groceries
ORDER BY aisle 
```


With conditions
```sql
/* WHERE */

SELECT *
FROM groceries
WHERE aisle > 5
```
```sql
/* IN */

SELECT *
FROM exercise_logs
WHERE type IN ("biking", "hiking", "tree climbing", "rowing");
```
```sql
/* NOT IN */

SELECT *
FROM exercise_logs
WHERE type NOT IN ("biking", "hiking", "tree climbing", "rowing");
```
```sql
/* AND */

SELECT *
FROM groceries
WHERE aisle > 5 AND quantity > 1
```
```sql
/* OR */

SELECT *
FROM groceries
WHERE aisle > 5 OR quantity >5
```

### SQL Subquery
```sql
SELECT *
FROM exercise_logs 
WHERE type IN (SELECT type 
		FROM drs_favorites);
```
```sql
/* LIKE */

SELECT * 
FROM exercise_logs 
WHERE type IN (SELECT type 
		FROM drs_favorites
		WHERE reason LIKE "%cardiovascular%");
```


## Aggregate Data

```sql
SELECT SUM(quantity)
FROM groceries;
```
```sql
SELECT MAX(quantity)
FROM groceries;
```
```sql
/* GROUP BY */

SELECT aisle, SUM(quantity)
FROM groceries
GROUP BY aisle;
```

### Restricting grouped results with HAVING
When using `HAVING`, the filtering applies to the grouping results.

When using `WHERE`, the filtering applies to the individual rows.

```sql
/* HAVING */

SELECT type, SUM(calories) AS total_calories FROM exercise_logs
    GROUP BY type
    HAVING total_calories > 150
```
![enter image description here](https://imgur.com/odJUNzO.png)

```sql
/* COUNT(*) */

SELECT type FROM exercise_logs
	GROUP BY type
	HAVING COUNT(*) >= 2;
```

## Calculating results with CASE

```sql
/* CASE */

SELECT type, heart_rate,
    CASE 
        WHEN heart_rate > 220-30 THEN "above max"
        WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
        ELSE "below target"
    END as "hr_zone"
FROM exercise_logs;
```
![enter image description here](https://i.imgur.com/hN0d9EI.png)

```sql
SELECT COUNT(*),
    CASE 
        WHEN heart_rate > 220-30 THEN "above max"
        WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
        ELSE "below target"
    END as "hr_zone"
FROM exercise_logs
GROUP BY hr_zone;
```
![enter image description here](https://i.imgur.com/BDt9dVm.png)

# Relational Queries in SQL
```sql
SELECT * FROM student_grades; 
SELECT * FROM students;
```

![enter image description here](https://i.imgur.com/OVbHsfR.png)

```sql
/* implicit inner join */
SELECT * FROM student_grades, students
    WHERE student_grades.student_id = students.id;
```

```sql
/* explicit inner join - JOIN */
SELECT * FROM students
    JOIN student_grades
    ON students.id = student_grades.student_id;
```

![enter image description here](https://i.imgur.com/LWqIe9U.png)

## Outer Join
The FULL _OUTER JOIN_ keyword returns all matching records from both tables whether the other table matches or not.

```sql
/* outer join - LEFT OUTER */ 
SELECT students.first_name, students.last_name, student_projects.title
    FROM students
    LEFT OUTER JOIN student_projects
    ON students.id = student_projects.student_id;
```

![enter image description here](https://i.imgur.com/eZu9Ct8.png)

## Self-Join

```sql
/* self join */
SELECT students.first_name, students.last_name, buddies.email as buddy_email
    FROM students
    JOIN students buddies
    ON students.buddy_id = buddies.id;
```

## Multiple Joins
```sql
SELECT a.fullname, b.fullname FROM friends
    JOIN persons a
    ON a.id = friends.person1_id
    JOIN persons b
    ON b.id = friends.person2_id
```

# Modifying databases with SQL
Update Operation
```sql
UPDATE diary_logs
	SET content = "I had a horrible fight with OhNoesGuy"
	WHERE id = 1;
```
Delete Operation
```sql
DELETE FROM diary_logs
	WHERE id = 1;
```

Altering tables after creation
```sql
ALTER TABLE diary_logs ADD emotion TEXT;
```

```sql
ALTER TABLE diary_logs ADD emotion TEXT default "unknown";
```

Delete the entire table
```sql
DROP TABLE diary_logs;
```

## Make your SQL safer

LIMIT operator

```sql
UPDATE users
	SET deleted = true
	WHERE id = 1
	LIMIT 1;
```

```sql
DELETE users
	WHERE id = 1
	LIMIT 1;
```


# References
Khan Academy
Intro to SQL: Querying and managing data
https://www.khanacademy.org/computing/computer-programming/sql



> Written with [StackEdit](https://stackedit.io/).
