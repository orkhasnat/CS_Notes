# Table of Contents
- [[#Functions]]
	1. [[#VLOOKUP]]
- [[#Date Validation with Drop-down Calendar Selector]]

---

## Functions
Remember, Parameters that look like this, `[parameter_name]` are optional.
> Complete Functions List [here](https://support.google.com/docs/table/25273?hl=en&ref_topic=9054531&sjid=14196954127541723202-AP).

##### VLOOKUP
VLOOKUP or vertical lookup function searches down the first column of a range for a key and returns the value of a specified cell in the row found.
> See in detail [here](https://support.google.com/docs/answer/3093318?sjid=14196954127541723202-AP).

```
VLOOKUP(search_key, range, index, [is_sorted])
```
Here, 
- `search_key`: The value to search for in the first column of the range.
- `range`: The upper and lower values to consider for the search. If it spans more than two column e.g. search key column in B and target key column in E, and it spans from row 3 to row 9, then pass `B3:E9`.
- `index`: The index of the column with the return value of the range. The index must be a positive integer. **The first column passed in the `range` is 1,not 0.** E.g. in the previous example, where `range` was from `B` to `E`, `index` would be 4 (`B->1, C->2, D->3, E->4`).
- `is_sorted` (Optional): `True`(1) or `False`(0). **Remember to always pass `False`, unless you know what you are doing.**
	- `FALSE` = Exact match. ***This is recommended.***
	- `TRUE` = Approximate match. This is the **default** if `is_sorted` is unspecified. Don't keep it empty unless you want to pass `True`. 
## Date Validation with Drop-down Calendar Selector
- First select the column and choose data validation.
- In the option part, choose `is valid date` from the drop-down menu.
- Now you have the option to select the date from calendar drop down.
- But the formatting would be bonked.
- So again select the column and go to `Format`>`Number`>`Custom Date and Time`
- Now choose the appropriate custom date settings

Thus the goal is achieved.