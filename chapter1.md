---
title: 'Lesson 1.3: Use Joins to Build a Basetable'
description: 'A good first step in any analysis is to put all the information you want to analyze in one place. Often as analysts, we work with data from a variety of sources - accessing different tables in an existing database architecture or collecting new information from open sources like government websites. This part of our case study will use joins to combine three tables into a single source of information for the rest of our project. '
---

## Use Joins to Build a Basetable

```yaml
type: VideoExercise
key: b1063de69e
xp: 50
```

`@projector_key`
263e607ea143a36f86dc93749736e53a

---

## Building Our Base Table

```yaml
type: NormalExercise
key: e8c1edbe67
lang: python
xp: 100
skills: 2
```

The example code from the previous slides shows two ways of combining the horserace and demographic questions. 

When we build our table, we'll use an inner join because we have complete data on all respondents for each variable in the two tables. Our issues questions were only asked in key districts, so we could write an inner join that only retains rows where a respondent was asked an issue question, but that would hinder our analysis of other districts. 

Instead we want to use a left join and retain all of our demographic and horserace questions while attaching all the issue questions we have to our base table. 

`@instructions`
Add a left join to our existing syntax joining the `issues` table to the existing combination of the `horserace` and `demographics` tables.

`@hint`
The unique identifier for all three tables is `respondent_id`

`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
select 
	*
from horserace h
inner join demographics d on h.respondent_id = d.respondent_id
__________ issues i __ h.respondent_id = __.___________
```

`@solution`
```{python}
select 
	*
from horserace h
inner join demographics d on h.respondent_id = d.respondent_id
left join issues i on h.respondent_id = i.respondent_id
```

`@sct`
```{python}

```
