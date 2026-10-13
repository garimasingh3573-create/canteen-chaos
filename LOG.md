# Debug log

Your notes. One entry per bug you fixed, using the template below.

This file is read as carefully as your code. A correct fix you cannot
explain counts for little; a bug you could not fix but investigated
honestly still counts for something.

Delete the example before you submit.



### CC-01 — "The search suggestions are behind everything"

**Reproduced:** Typed `be` in the search box. The suggestions appeared,
but the category bar covered the lower part of the list, making the lower
suggestions difficult to click.

**Cause:** `.search-wrap` had `z-index: 1`, while the filter/category area
had a higher stacking level. The suggestion box's `z-index: 100` could not
escape its parent stacking level.

**Fix:** Changed `.search-wrap` to `z-index: 50` in `frontend/style.css`,
placing the complete search area above the category bar.

**Checked:** Refreshed the page and searched for `be`. The complete
suggestions list appeared above the category bar.

**Time:** Not recorded.



### CC-02 — "Can't read anything in dark mode"

**Reproduced:** In dark mode, the dish names and prices were very hard to
read. In light mode, they were easy to read.

**Cause:** The dish card used a fixed dark text color. It stayed dark when
the theme changed to dark mode.

**Fix:** Changed the dish card text color to `var(--ink)` in
`frontend/style.css`. This variable changes with the theme.

**Checked:** Refreshed the page in dark mode. Dish names and prices were
clear and readable.

**Time:** Not recorded.



## Could not fix

For anything you investigated but did not solve. Say what you tried and
where you got to. This is worth marks — leaving it blank when you got
stuck is not.

### CC-0X — "<the complaint>"

**What I tried:**

**Where I got to:**

**What I would try next:**



## Extra credit

Anything not on the bug log: a problem you found yourself, a test you
wrote, or a fix you are unsure about. Same format, plus one line on how
you noticed it.
