# SQL
- Structured Query Language: declarative programming paradigm (describes what you want to achieve wo too much detail on how)

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
