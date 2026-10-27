# Arrays and Dot Product Checkpoint

Pseudocode solutions to both GoMyCode problems, using arrays and nested loops.

## Problem 1: Sum of distinct elements

See [problem-1.txt](problem-1.txt).

The supplied example and instructions mean elements present in **only one** set (the symmetric difference). Elements shared by both sets are excluded. This differs from summing the whole union.

The algorithm starts with `sum = 0`, compares every element of the first array with the second, and adds it only if it is absent. It then repeats the comparison in the other direction.

For `[3, 1, 7, 9]` and `[2, 4, 1, 9, 3]`, the included elements are `7`, `2`, and `4`, so the result is **13**.

Assumption: as the problem describes sets, each input array has no repeated elements within itself. Values can still appear in both arrays. Empty sets have size zero; a loop with an upper bound below its starting value performs no iterations.

## Problem 2: Dot product and orthogonality

- [Procedure version](problem-2-procedure.txt)
- [Function version](problem-2-function.txt)

Both versions calculate:

`ps = v1[1] * v2[1] + ... + v1[dimension] * v2[dimension]`

For each of `n` vector pairs, the main algorithm reads the common dimension, reads both arrays in an inner loop, calculates the dot product, and reports whether it is zero. Each vector pair can have a different dimension; the two vectors within a pair must have the same dimension.

### Parameter passing

| Parameter | Mode | Purpose |
| --- | --- | --- |
| `v1`, `v2` | IN, by value | Supply vector coordinates without changing the caller's arrays |
| `dimension` | IN, by value | Supply the common vector length |
| `ps` in the procedure | OUT, by reference | Store the calculated result in the caller's variable |
| Function result | Return value | Assigned to `ps` by the caller |

The procedure is invoked with `CALL dot_product(v1, v2, dimension, ps)`. The function is used in an assignment: `ps <- dot_product(v1, v2, dimension)`.

## Pseudocode conventions

Arrays use indices starting at 1. `DECLARE array[1..size]` allocates an array after its size has been read. Input sizes are non-negative integers, vector dimensions are positive integers, and coordinates are real numbers. `READ` reads one specified value. The notation is language-independent pseudocode, not executable JavaScript.

The mathematical orthogonality test is `ps = 0`, as requested. A numerical implementation using floating-point decimals may need an absolute or relative tolerance because arithmetic can round results.

## Verified examples

### Distinct-element sum

| First set | Second set | Result |
| --- | --- | --- |
| `[3, 1, 7, 9]` | `[2, 4, 1, 9, 3]` | 13 |
| `[1, 2]` | `[1, 2]` | 0 |
| `[1, 2]` | `[3, 4]` | 10 |
| `[]` | `[5]` | 5 |

### Dot product

These three rows can be supplied as three successive vector pairs (`n = 3`). Both versions produce the same results.

| v1 | v2 | ps | Orthogonal? |
| --- | --- | --- | --- |
| `[1, 2]` | `[2, -1]` | 0 | Yes |
| `[1, 2, 3]` | `[4, 5, 6]` | 32 | No |
| `[0, 0]` | `[3, 4]` | 0 | Yes |
