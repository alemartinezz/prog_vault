# SQL

## Multiple SQL updates

```sql
UPDATE categories
SET priority = CASE
    WHEN name = 'Hair' THEN 1
    WHEN name = 'Men''s Styling' THEN 2
    WHEN name = 'Lashes' THEN 3
    WHEN name = 'Spa' THEN 4
    WHEN name = 'Tanning' THEN 5
    WHEN name = 'Waxing' THEN 6
    WHEN name = 'Nails' THEN 7
    WHEN name = 'Eyebrows' THEN 8
    WHEN name = 'Skincare' THEN 9
    WHEN name = 'Sugraring' THEN 10
    WHEN name = 'Threading' THEN 11
    WHEN name = 'Make Up' THEN NULL
    ELSE priority -- Leave the priority as is if none of the conditions are met
END
WHERE name IN ('Hair', 'Men''s Styling', 'Lashes', 'Spa', 'Tanning', 'Waxing', 'Nails', 'Eyebrows', 'Skincare', 'Sugraring', 'Threading', 'Make Up');
```
