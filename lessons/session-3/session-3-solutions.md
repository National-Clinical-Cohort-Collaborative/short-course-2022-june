Solutions to Session 3 Exercises
=============

Notes

* Please make sure that the transforms are named *exactly* `exercise_3`, `exercise_4`, and `exercise_5`.  Pay attention to spaces, underscores, and capitalization.

Exercise 3
-----------------

The "exercise_3" sql transform in the "Malnutrition Conditions" workbook currently produces 10 columns & 1 row.

```sql
SELECT 
  *
FROM concept
WHERE 
  vocabulary_id = 'SNOMED'
  and
  concept_code = '70241007'
```

Exercise 4
-----------------

The "exercise_4" sql transform in the "Malnutrition Conditions" workbook currently produces 4 columns & 166 rows.

```sql
SELECT 
  *
FROM concept_ancestor
WHERE 
  ancestor_concept_id = 435227
```

Exercise 5
-----------------

The "exercise_5" sql transform in the "Malnutrition Conditions" workbook currently produces 1 column & 166 rows.

```sql
SELECT
  e4.descendant_concept_id
FROM exercise_4 e4
  inner join concept c on e4.descendant_concept_id = c.concept_id
WHERE c.standard_concept = 'S'
```

Exercise 6
-----------------

The "exercise_6" sql transform in the "Malnutrition Conditions" workbook currently produces 21 columns & 16,149 rows.

```sql
SELECT 
  co.*
FROM condition_occurrence co
  inner join exercise_5 e5 on 
    e5.descendant_concept_id = co.condition_concept_id
    and
    co.data_partner_id = 198
    and
    co.condition_start_date < '2020-01-01'
```
