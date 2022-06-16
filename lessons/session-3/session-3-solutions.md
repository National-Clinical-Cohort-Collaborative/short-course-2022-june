Solutions to Session 3 Exercises
=============

Exercise 3
-----------------

"exercise 3" sql transform in the "Malnutrition Conditions" workbook

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

"exercise 4" sql transform in the "Malnutrition Conditions" workbook

```sql
SELECT 
  *
FROM concept_ancestor
WHERE 
  ancestor_concept_id = 435227
```

Exercise 5
-----------------

"exercise_5" sql transform in the "Malnutrition Conditions" workbook

```sql
SELECT
  e4.descendant_concept_id
FROM exercise_4 e4
  inner join concept c on e4.descendant_concept_id = c.concept_id
WHERE c.standard_concept = 'S'
```
