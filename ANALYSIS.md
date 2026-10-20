# Vector and Scalar Evaluation

We used this given input: c(Blossom=NA, Bubbles=15, Buttercup=6). In the `clean_scores_vector` function, it first sets NA to 0 with the line `scores[is.na(scores)] <- 0`. Then, it multiplies each element by 2, resulting in [0,30,12]. Next, the line `scores[scores>20] <- 20` caps any values over 20 by reassigning them, so, in this case, 30 becomes 20, and the vector becomes [0,20,12]. 

As for `clean_scores_scalar`, it returns the same vector but handles it in a different way. It loops through each element and checks for missing values first. On pass 1, Blossom=NA becomes 0 and the remaining operations in the else branch are skipped. Passes 2 and 3 go to the else branch, where the scores are doubled, resulting in Bubbles=30 (which gets capped at 20 by the succeeding if statement) and Buttercup=12. This results in the same vector, [0, 20, 12]. 

In the vector version, the three operations that act on all elements at once are `scores[is.na(scores)] <- 0` (sets missing values to 0), `scores <- scores*2` (multiplies scores by 2), and `scores[scores>20] <- 20` (caps max values at 20). These expressions demonstrate logical indexing, subassignment, vectorized arithmetic, and comparison. 

In the scalar version,  the evaluation order becomes visible as the for loop processes one element per iteration. The if and else statements make the order explicit. When the loop encounters a missing value, the value becomes zero and the remaining operations in the else branch are skipped. Otherwise, the value is doubled and compared with the cap of 20. If the doubled value exceeds 20, it is reassigned to 20. 

For recycling, let's say we want different caps for each person, so we create a vector `c(20, 15)`, though it should be `c(20, 15, 18)`, and apply it to the scores vector. If the caps vector has fewer values than the scores vector, R recycles it instead of failing. So in this example, assuming all three doubled scores are greater than their caps, the result would be [20, 15, 20] because the caps recycle onto Buttercup's score, giving her Blossom's cap of 20 instead of 18. This demonstrates how careless recycling can produce incorrect results without an error. 

Personally, we would choose the vector implementation since it's shorter and has a faster running time. Though it is not without tradeoffs, since it makes evaluation invisible and possible recycling mistakes might happen silently.
