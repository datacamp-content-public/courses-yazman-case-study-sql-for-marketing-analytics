---
title: 'Lesson 2: Summarising Data With Grouping and Aggregation'
description: ""
---

## Explore the data for yourself

```yaml
type: NormalExercise
key: f030cd632e
xp: 100
```

During this project, we decided to poll some areas multiple times to see if product preferences changed over time. The `poll_id` field in the `upshot_polling_base` table tells us which poll is which when the same district is polled multiple times.

`@instructions`
Fill in the blanks to aggregate support for `Product A` and `Product B` partitioning the query so summary calculations are performed for each poll separately.

`@hint`
Group by the field that we want to compare results for (ie: which product a consumer prefers) and partition by the field that differentiates the separate groups we want to calculate results for.

`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
select 
        poll_id
        , product_preference
        , round(sum(w_buyer)*100/sum(sum(w_buyer)) over(partition by _____)) as percent_support
from upshot_polling_base
where district = 'fl26'
group by ________, ________
having response in ('Und','A','B')
order by 1,2;
```

`@solution`
```{python}
select 
        poll_id
        , product_preference
        , round(sum(w_buyer)*100/sum(sum(w_buyer)) over(partition by poll_id)) as percent_support
from upshot_polling_base
where district = 'fl26'
group by poll_id, product_preference
having response in ('Und','A','B')
order by 1,2;
```

`@sct`
```{python}

```
