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



### CC-03 — "The menu is wider than my phone"

**Reproduced:** Set the mobile screen width to `320px` and searched for
`Paneer Butter Masala`. The long name and the right side of the card were
cut off.

**Cause:** On small screens, the dish name button used `width: max-content`.
This made it as wide as the full name.

**Fix:** Changed the mobile rule to `width: 100%; min-width: 0` in
`frontend/style.css`. The name can now wrap inside the card.

**Checked:** Tested again at `320px`. The name wrapped and the full
`Add to Cart` button was visible.

**Time:** Not recorded.



### CC-04 — "The buttons don't work on my tablet"

**Reproduced:** Opened the app in iPad Mini view. The **Add to Cart** and
star buttons did not respond.

**Cause:** Invisible layers were placed over the dish cards on tablet
screens. These layers received the clicks.

**Fix:** Added `pointer-events: none` to the invisible tablet layers in
`frontend/style.css`. They now ignore clicks.

**Checked:** Refreshed the iPad Mini view. The cart count increased and the
star showed a saved message.

**Time:** Not recorded.



### CC-05 — "The category bar scrolls away on my phone"

**Reproduced:** Opened the app in iPhone SE view and scrolled down. The
filter and category bar disappeared.

**Cause:** The mobile view used `overflow-x: hidden`. This stopped the
sticky bar from using the browser page as its scrolling area.

**Fix:** Changed it to `overflow-x: clip` in `frontend/style.css`. This
still hides sideways overflow without breaking the sticky bar.

**Checked:** Refreshed the phone view and scrolled again. The filter and
category bar stayed visible.

**Time:** Not recorded.



### CC-06 — "I ordered more than they had"

**Reproduced:** A dish showed `Only 3 left`. I added 4 to the cart and
the order was accepted.

**Cause:** The backend only checked if stock was zero. It did not compare
the requested quantity with the stock.

**Fix:** Added a backend check in `backend/logic/validation.js`. An order
is rejected when its quantity is greater than the stock. Also added a
frontend check in `frontend/js/state.js`, so the `+` button cannot increase
the quantity above the stock.

**Checked:** With 3 items in stock, the cart stopped at 3 and showed
`Only 3 left` when I tried to add a fourth. The backend also rejected an
order that went over the stock limit.

**Time:** Not recorded.



### CC-07 — "Cancelling makes it worse"

**Reproduced:** Rajma Chawal had 25 items. I ordered one, so it became
24. After cancelling the order, it became 23 instead of returning to 25.

**Cause:** The cancellation code subtracted the cancelled quantity from
stock. It should add the quantity back.

**Fix:** Changed the cancellation calculation in
`backend/logic/validation.js` from subtraction to addition.

**Checked:** Ordered and cancelled one Rajma Chawal. Stock returned to 25.

**Time:** Not recorded.



### Supporting fix — "My Orders showed no orders"

**Reproduced:** Placed an order and opened **My Orders**. The page said
`No orders found`, even though the browser had saved order tokens.

**Cause:** The browser sent `memberId`, but the backend compared it with
`userId`. The names did not match.

**Fix:** Changed the backend to compare orders with `req.query.memberId` in
`backend/routes/orders.routes.js`.

**Checked:** Restarted the server and opened **My Orders**. The saved orders
appeared.

**Time:** Not recorded.



### CC-08 — "An old coupon still works"

**Reproduced:** Added a dish and applied `FRESHERS24`. The coupon was
expired, but the app still gave a discount.

**Cause:** The pricing code did not check the coupon expiry date.

**Fix:** Added an expiry-date check in `backend/logic/pricing.js`. Expired
coupons are now rejected.

**Checked:** Applied `FRESHERS24` again. The app showed `This coupon has
expired` and did not reduce the total.

**Time:** Not recorded.



### CC-09 — "The menu shows more dishes than it should"

**Reproduced:** The menu requested 5 dishes, but it showed all 37 dishes
at once.

**Cause:** The pagination code made a 5-dish list but returned the original
full list instead.

**Fix:** Changed the returned value from `items: list` to `items` in
`backend/logic/search.js`.

**Checked:** Refreshed the page. It showed 5 dishes and total 37. More
dishes can load while scrolling.

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
