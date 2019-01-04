---
title: 'Subqueries and Unions'
description: ""
---

## Explore how opinions on Gushers impacts product preferences

```yaml
type: NormalExercise
key: 280f8d06df
xp: 100
```

Often when we conduct surveys, we want to reformat the response data so comparisons across conditions are easier. For example, we could produce a results summary that simply aggregates `gushers_are_ravioli` by district. The `WITH` portion of the sample code does this. 

`@instructions`
Next we want to create a column for each of the two major response options and an additional column showing the percentage of consumers who support the statement that Gushers are Ravioli (`gushers_are_ravioli = 'Support`) minus the percentage of consumers who oppose this statement (`gushers_are_ravioli = 'Oppose`).

`@hint`


`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
WITH prod_pref AS (
        SELECT district
                , check_or_support
                , ROUND(SUM(w_buyer)*100/SUM(SUM(w_buyer)) OVER(partition by district),1) AS pct_support
        FROM upshot_polling_base
        WHERE gushers_are_ravioli IN ('Support','Check')
        group by 1,2)
SELECT s.district
        , s.percent_support
        , o.percent_check
        , round(s._____ - o._____, 1) AS margin
FROM (select district, pct_support FROM prod_pref where _________ = '_________') s
INNER JOIN (select district, pct_support AS percent_check FROM prod_pref where _________ = '_________') o ON s.district = c.district
ORDER BY margin DESC;
```

`@solution`
```{python}
WITH prod_pref AS (
        SELECT district
                , gushers_are_ravioli
                , ROUND(SUM(w_buyer)*100/SUM(SUM(w_buyer)) OVER(partition by district),1) AS pct_support
        FROM upshot_polling_base
        WHERE gushers_are_ravioli IN ('Support','Check')
        group by 1,2)
SELECT s.district
        , percent_support
        , percent_check
        , round(percent_support - percent_check, 1) AS margin
FROM (select district, pct_support as percent_support FROM prod_pref where gushers_are_ravioli = 'Support') s
INNER JOIN (select district, pct_support AS percent_check FROM prod_pref where gushers_are_ravioli = 'Oppose') c ON s.district = c.district
ORDER BY margin DESC;
```

`@sct`
```{python}

```
