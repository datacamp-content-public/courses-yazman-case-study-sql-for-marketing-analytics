---
title: 'Case Statements and Unions'
description: ""
---

## Build Survey Crosstabs

```yaml
type: NormalExercise
key: 4f8ebf7fd2
xp: 100
```

As a final step in preparing our data for a full analysis, we want to produce crosstabs comparing responses to key questions across the various categories of consumers we've surveyed. To do this, we'll create a series of small summary tables, and union them together. 

`@instructions`
Fill in the blanks in the SQL code to produce the second summary results table and union it to the first one

`@hint`


`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
select 1 as group_order
        ,gender as group_name
        , round(sum(case when product_preference = 'A' then w_buyer else 0 end)*100/sum(w_buyer)) as product_a_support
        , round(sum(case when product_preference = 'B' then w_buyer else 0 end)*100/sum(w_buyer)) as product_b_support
from upshot_polling_base
where product_preference in ('A','B') and district = 'va10'
group by 1, 2
_______
select 2 as group_order
        , age as group_name
        , round(sum(case when product_preference = '___' then w_buyer else 0 end)*100/sum(w_buyer)) as product_a_support
        , round(sum(case when product_preference = '___' then w_buyer else 0 end)*100/sum(w_buyer)) as product_b_support
from upshot_polling_base
where product_preference in ('A','B') and district = 'va10'
group by 1, 2
```

`@solution`
```{python}
select 1 as group_order
        ,gender as group_name
        , round(sum(case when product_preference = 'A' then w_buyer else 0 end)*100/sum(w_buyer)) as product_a_support
        , round(sum(case when product_preference = 'B' then w_buyer else 0 end)*100/sum(w_buyer)) as product_b_support
from upshot_polling_base
where product_preference in ('A','B') and district = 'va10'
group by 1, 2
union
select 2 as group_order
        , age as group_name
        , round(sum(case when product_preference = 'A' then w_buyer else 0 end)*100/sum(w_buyer)) as product_a_support
        , round(sum(case when product_preference = 'B' then w_buyer else 0 end)*100/sum(w_buyer)) as product_b_support
from upshot_polling_base
where product_preference in ('A','B') and district = 'va10'
group by 1, 2
```

`@sct`
```{python}

```
