# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a
later commit.

## P01
Atomic vectors must have their values all of the same mode. Specifically, type coercion in atomic vectors : logical types are casted to doulbe when a double is present. Vector lengths are just the number of elements present in the 1D vector.

## P02
When a string is present in an atomic vector, all other elements are casted to character type and are surrounded by `"` or `'`. 

## P03
Vector arithmetic where operations are performed element by element, wherein recycling occurs where the shorter vector is repeated in order until it matches the length of the other vector. The type preserved belongs is of the vector with the highest type coercion, whereas the length are from the longer of the two. Dim remains none.

## P04
Positive index vector and naming (each element can be given a name). The corresponding elements of the vector are selected and concatenated, in that order, in the result and preserves the source vector's type and the extracted elements' name and value. Dim remains none and length is the number of elements produced.

## P05
Negative index in vectors, which specifies the values to be excluded rather than included. Type, dim, and the extracted elements' name, value, and order remains the same as the source vector. Length is determined by the number of elements from the produced vector.

## P06
Logical index vector. | computes the logical at every position, where values corresponding to TRUE in the index vector are selected and those corresponding to FALSE are omitted. Type is preserved, with length being the resulting number of elements of the produced vector. 

## P07
Factor declaration which is built on top of integers, with two attributes: a class, “factor”, which makes it behave differently from regular integer vectors, and levels, which defines the set of allowed values. Type is integer because it is an integer vector, has no dim.

## P08
List declaration with elements being of any type, which is just a reference to another object of any type - hence its type remains as list. Length is 2 because it has two elements: scores and label. Dim is none because lists are almost always 1D.
Correction: lists have no dim attributes.

## P09
Data frame declaration. It is simply a list with a class attribute, hence typeof() returns a list. Length is the number of columns, dim is always 2 (columns and rows). 

## P10
Matrix declaration, basically just a vector with elements being split into rows - thus its length is the number of elements in the matrix which is 6. Recycling occurs during arithmetic operations where the vector's elements are repeated to match until the end of the matrix. A matrix is a 2D array, hence its dim is 2 with type being integer because arrays must always have their elements of the same type.

## P11
Function call that evaluates based on the provided vector input and produces a vector as a result. Mean expects a numeric type for all values, but reads a missing value and returns NA as it cannot evaluate with a missing value - which is still an element, hence length is 1. Since the type of the elements from the source vector are double, the output type is also double despite being missing.

## P12
na.rm = TRUE evaluates the input vector by dropping values whose values are NA. The resulting input vector after the filter is [8, 10], therefore mean is calculated by the sum of its elements (8+10) divided by the number of elements (2).

## P13
Initializes an integer vector `x` with three elements [1,2,3], then updates the 2nd element with 2.5 which triggers type coercion that widens `x` into a double vector.

## P14
Initializes an integer vector `scores` with four elements [7, NA_real_, 12, 4], which is fed into ifelse(is.na(scores), 0, scores*2) to make one choice per position and produces [14, 0, 24, 8] as an integer vector to `adjusted`. `adjusted` is then evaluated with a logical index that replaces elements whose value > 15 to 15. Hence, `adjusted` is produced as a length four integer vector [14,0,15,8]. Correction: we predicted it to be integer but NA is a double and the other values doesn't have an L which indicates also being a double

## P15
Array declaration that with dimension set to 2x2x2 with elements set from 1 to 8.

## P16
Index 0 selects nothing and returns a zero-length result of the same atomic type.