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

---

## Lesson 1 Capstone

```yaml
type: NormalExercise
key: 908beb9718
xp: 100
```

In our final exercise for chapter 1, we want to use joins to combine our three tables into one base file to simplify the rest of our analysis. Recall that we have three tables containing horserace numbers, demographic data, and a set of specific questions asked only for a subset of survey respondents.  

`@instructions`
In the exercise, choose the type of join that's most appropriate to add `issues` to our existing base file. Make sure the variables in your `select` clause appropriately reference the

`@hint`
An `inner join` will return rows for the combined table where `respondent_id` matches in _both_ tables. A `left join` will return all rows from the left table plus any rows that match from the right table.

`@pre_exercise_code`
```{python}
connect('postgresql', 'marketing_case_sql_upload')
set_options(visible_tables = ['horserace', 'demographics', 'issues'])
```

`@sample_code`
```{python}
CREATE TABLE upshot_polling_base as(
        SELECT h.*
                , d.race_eth
                , d.gender
                , d.age
                , d.education
                , d.party
                , d.region
                , d.turnout
                , _.hotdogs_are_sandwiches
                , _.gushers_are_ravioli
        FROM horserace h
        INNER JOIN demographics d ON h.respondent_id = d.respondent_id 
        _____ JOIN  issues i ON _.____________ = _.____________);
```

`@solution`
```{python}
create table upshot_polling_base as(
        select 
                h.*
                , d.race_eth
                , d.gender
                , d.age
                , d.education
                , d.party
                , d.region
                , d.turnout
                , i.hotdogs_are_sandwiches
                , i.gushers_are_ravioli
        from horserace h
        inner join demographics d on h.respondent_id = d.respondent_id 
        left join issues i on h.respondent_id = i.respondent_id);
```

`@sct`
```{python}

```
