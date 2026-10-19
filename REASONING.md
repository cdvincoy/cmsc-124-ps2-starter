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

The object has class data.frame and type list, containing two named columns, `id` and `passed`. The id column has type integer, while the passed column has type logical. The object has a length of two(columns) and dimensions of 2x2.

## P10

`matrix(1:6, nrow = 2L)` takes six values and builds an integer vector with 3 columns and 2 rows, so it is stored as 1 2 3 4 5 6 alternatively being assigned top then bottom with dim 2 by 3. Adding `c(10L, 20L)` recycles down that stored order, so 10 goes to the top row and 20 to the bottom row. Integer plus integer stays integer, so the value is [11,22,13,24,15,26] with type integer, length 6, and dim 2x3.

## P11

Generally, any operation on NA becomes an NA, which includes the mean operation; so, the NA in the second position makes the mean NA. Numeric calculations are done in double precision, so the result is double. The value is [NA], with length 1 and no dimensions.

## P12

The previous case mentioned that any operation that has an NA would convert it into an NA, but the `na.rm` argument removes missing values before any operation can run. The resulting vector becomes `c(8,10)`, which has a mean of 9 as its value, double as its type, a length of 1 and no dimension.

## P13

The expressions are grouped in a block using braces and evaluated from top to bottom. The second element is replaced with 2.5, causing the integer vector to be coerced to type double. The resulting vector is [1,2.5,3], with type double, a length of three, and no dimensions.

## P14

The expressions are grouped in a block using braces and evaluated from top to bottom. The ifelse(test, yes, no) function replaces the missing value with 0 and multiplies the other values by 2 and conditional indexing then replaces values greater than 15 with 15. The resulting vector is [14,0,15,8] with type double, a length of four and no dimensions. 

## P15

The object has class array and type integer because 1:8 creates an integer vector. The dim argument arranges the eight values into an array with three dimensions. The array has a length of eight and dimensions of 2x2x2.

## P16

The original vector has type integer, a length of three, and no dimensions. Indexing with 0L selects no elements and returns a zero-length vector of the same type. The resulting value is [], with type integer, a length of zero, and no dimensions.