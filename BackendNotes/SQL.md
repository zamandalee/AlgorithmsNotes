# SQL
- Structured Query Language: declarative programming paradigm (describes what you want to achieve wo too much detail on how)

## ```JOIN```s
- ```INNER JOIN```: only records that match in both tables
- ```FULL OUTER JOIN```: all records, where there's no match the missing table contains null
- ```LEFT OUTER JOIN```: all records from SELECTed table, matches from right table, null where no match
  ```sql
  -- left + overlap of Venn diagram
  SELECT * FROM TableA
  LEFT OUTER JOIN TableB
  ON TableA.name = TableB.name

  -- left, no overlap
  SELECT * FROM TableA
  LEFT OUTER JOIN TableB
  ON TableA.name = TableB.name
  WHERE TableB.id IS null
  ```
- ```FULL OUTER JOIN```: unique records
  ```sql
  -- left + right, no overlap
  SELECT * FROM TableA
  FULL OUTER JOIN TableB
  ON TableA.name = TableB.name
  WHERE TableA.id IS null
  OR TableB.id IS null
  ```
- Self ```JOIN```: like join between 2 identical copies of table
  ```sql
  -- table has first_name, last_name, manager_id
  SELECT
    team_member.first_name, team_member.last_name,
    manager.first_name, manager.last_name
  FROM
    employee AS team_member
  JOIN
    employee AS manager ON manager.id = team_member.manager_id
  ```

## ```INSERT```
```sql
INSERT INTO
  users (name, age, height_in_inches)
VALUES
  ('Santa Claus', 876, 34);
```

## ```UPDATE```
```sql
UPDATE
  users
SET
  name = 'Eddard Stark', house = 'Winterfell'
WHERE
  name = 'Ned Stark';
```

## ```DELETE```
```sql
DELETE FROM
  users
WHERE
  (name = 'Eddard Stark' AND house = 'Winterfell');
```

Great Sources:
https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/
