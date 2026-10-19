# Vector and Scalar Evaluation

Take `c(Ada = 8, Grace = NA, Linus = 12, Barbara = 4)`. In `clean_scores_vector()`, `is.na(scores)` produces the mask `FALSE`, `TRUE`, `FALSE`, `FALSE`. `if/else` then picks `0` at Grace's position and `(scores * 2)` elsewhere, giving `16`, `0`, `24`, and `8` respectively. The mask `adjusted > 20` is `FALSE`, `FALSE`, `TRUE`, `FALSE`, so subassignment caps only Linus at 20. In `clean_scores_scalar()`, the loop reaches Grace on pass 2. `is.na(scores[i])` is `TRUE`, so `out[i] <- 0` runs and the doubling is skipped. The cap test then sees `0`, which is not above `20`. Both functions return `16, 0, 20, 8` with names attached.

In the vector version, `is.na(scores)`, `(scores * 2)`, the `if/else` selection, the comparison `adjusted > 20`, and the masked assignment each act on every element in one expression.

The loop makes order visible in each line, if the cap test ran before the `NA` check, `out[i] > 20` would be `NA` on pass 2 and it would stop with an error, so the `if/else` has to handle missing values first. The vector version has no order of events as the assignments act on all elements at once.

Suppose someone zeroes the missing score with `adjusted[c(FALSE, TRUE)] <- 0`. R recycles the mask to `FALSE, TRUE, FALSE, TRUE`, so Barbara's `8` becomes `0` as well. The result is `16, 0, 20, 0` instead of `16, 0, 20, 8`. It copies the boolean elements until it matches the length of the longer vector which gives wrong output. Our code avoids this because `is.na(scores)` always has the same length as scores.

We would keep `clean_scores_vector()`. It is shorter, preserves names automatically, and needs no counter to stay correct. The tradeoff is that R evaluates both conditions of `if/else`, executes `scores * 2` for every element, including the missing one, then discards the unused results, and we cannot step through one score at a time. The loop is easier to trace, but it takes more lines.
