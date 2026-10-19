# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a
later commit.

## P01

Based on the coercion ladder, which runs from logical to integer to double to character, `TRUE` and `2L` are coerced to double because `3.5` is a double. `TRUE` (logical) becomes `1.0` and `2L` (integer) becomes `2.0`. In other words, the value is [1,2,3.5]. It has a length of 3 and no dimensions.

## P02

The coercion ladder rule runs logical, integer, double, character. The second value is a character, so `1L` becomes `"1"` and `TRUE` becomes `"TRUE"`, with the result being a character. The value is ["1","2","TRUE"] with length 3 and no dimension.

## P03

This case involves arithmetics with two unequal but divisible length, so the shorter vector recycles to length 4, which will be added to the longer vector. This results in `10L + 1L`, `20L + 2L`, `30L + 1L`, `40L + 2L`, which is a value of [11,22,31,42] with length 4 and no dimensions. For its type, adding integer and integer always results in an integer as well, so need need for the coercion ladder rule for this case.

## P04

The positive indices in c(3L, 1L) select by position, in the order given, so the result takes the third element and then the first. Subsetting keeps the type, so the result stays integer. The value is [9,8] with length 2 and no dimensions.

## P05

The negative index in excludes that position, so [-2L] drops the second element, 7L. Subsetting keeps the type, so the result stays integer. The value is [4,9] with length 2 and no dimensions.

## P06

`NA_integer_` puts a missing integer in position two, so `is.na(x)` is `TRUE` only there, and `x > 10L` gives [FALSE NA TRUE FALSE], so `TRUE | NA` is `TRUE` (the known operand decides) and the index becomes [FALSE TRUE TRUE FALSE]. Logical indexing returns the elements at the TRUE positions, `NA` and `12L`, so the type stays integer. The value is [NA,12] with length 2 and no dimensions.

## P07

`levels = c("low", "high")` sets the category order, so `low` is code `1` and `high` is code `2`, and each element is replaced by the position of its label in that order. A factor stores integer codes plus level labels, so the type is integer. The value is [1,2,1] with length 3 and no dimensions.

## P08

A list keeps each component's own type, so no coercion happens. The two components are `scores` with the integer vector `3` and `5`, and `label`, the `string "A"` with value of [[3,5],"A"]. The type is list with length 2, which counts components rather than the individual values inside them, and there are no dimensions.

## P09

A data frame is a list with the constraint that its columns must be of equal length, so no coercion happens and each column keeps its own type. The columns are `id`, which is an integer vector with `1` and `2`, and passed, which is a logical vector with `TRUE` and `FALSE`. The type is list with value [[1,2],[TRUE,FALSE]], length 2 (which counts columns instead of individual elements) and dim 2x2.

## P10

`matrix(1:6, nrow = 2L)` takes six values and builds an integer vector with 3 columns and 2 rows, so it is stored as 1 2 3 4 5 6 alternatively being assigned top then bottom with dim 2 by 3. Adding `c(10L, 20L)` recycles down that stored order, so 10 goes to the top row and 20 to the bottom row. Integer plus integer stays integer, so the value is [11,22,13,24,15,26] with type integer, length 2, and dim 2x3.

## P11

Generally, any operation on NA becomes an NA, which includes the mean operation; so, the NA in the seocnd position makes the mean NA. Numeric calculations are done in double precision, so the result is double. The value is [NA], with length 1 and no dimensions.

## P12

The previous case mentioned that any operation that has an NA would convert it into an NA, but the `na.rm` argument removes missing values before any operation can run. The resulting vector becomes `c(8,10)`, which has a mean of 9 as its value, double as its type, a length of 1 and no dimension.

## P13

Assigning the double `2.5` into the second position is a mixed-mode assignment, it automatically widens the whole vector to double, including the untouched 1 and 3. So, the value becomes [1,2.5,3] with type double, length 3, and no dimensions.

## P14

## P14

`is.na(scores)` gives [F, T, F, F], and `ifelse` returns a vector the same length as the condition, taking a[i] (0) where it is true and b[i] (`scores * 2`) otherwise, so the NA position takes 0 and the rest take `scores * 2`, giving [14, 0, 24, 8]. The logical index adjusted > 15 is true only at the third position so subassignment replaces 24 with 15. All values are double, so the result is [14,0,15,8] with type double, length four, and no dimensions.

## P15

the array is filled with integers [1,2,3,4,5,6,7,8] with dimensions 2 by 2 by 2 assigned by `c(2L, 2L, 2L)`. Since 1:8 is integer and array() keeps the type, it will remain as integer. The value is [1,2,3,4,5,6,7,8] with type integer, length 8, and dim 2x2x2.

## P16

Index 0 selects nothing, so the result is a zero-length vector of the same type. The original is integer, so the result is an empty integer vector. The value is [] with type integer, length zero, and no dimensions.
