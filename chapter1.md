---
title: Tab Exercises
description: This chapter deals with another type of multi-step exercise called Tab Exercise and its variants.
---

## Single Hierarchical Clustering

```yaml
type: TabExercise
xp: 100
key: aec26f6a30
```

Let's return to the Olympic records example. You've already clustered the countries using the k-means algorithm, but this gave you a fixed amount of clusters. We're interested in more!

In this exercise, you'll apply the hierarchical method to cluster the countries. Of course, you'll be working with the standardized data. Make sure to visualize your results!

`@pre_exercise_code`

```{r, eval=FALSE}
run_record <- read.csv(url('http://s3.amazonaws.com/assets.datacamp.com/course/intro_to_ml/run_record.csv'), header = TRUE, row.names = 1)
run_record_sc <- as.data.frame(scale(run_record))
```

***

```yaml
type: NormalExercise
xp: 20
key: b25b64d284
```

`@instructions`

Calculate the Euclidean distance matrix of `run_record_sc` using [`dist()`](http://www.rdocumentation.org/packages/stats/functions/dist). Assign it to `run_dist`. [`dist()`](http://www.rdocumentation.org/packages/stats/functions/dist) uses the Euclidean method by default.

`@hint`

[`dist()`](http://www.rdocumentation.org/packages/stats/functions/dist) requires a dataset and a method argument.


`@sample_code`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist


```

`@solution`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

```

`@sct`
```{r, eval=FALSE}
msg <- "Do not remove or overwrite the predefined variables."
test_object("run_record", undefined_msg = msg, incorrect_msg = msg)
test_object("run_record_sc", undefined_msg = msg, incorrect_msg = msg)

test_object("run_dist", 
            undefined_msg = "You forgot to calculate the distance matrix or assign it to <code>run_dist</code>", 
            incorrect_msg = "Did you use <code>run_record_sc</code> in <code>dist()</code>?")

```

***

```yaml
type: NormalExercise
xp: 20
key: 38f93a8ff6
```

`@instructions`

Use the `run_dist` matrix to cluster your data hierarchically, based on single-linkage. Use [`hclust()`](http://www.rdocumentation.org/packages/stats/functions/hclust) with two arguments. Assign it to `run_single`.

`@hint`

The [`hclust()`](http://www.rdocumentation.org/packages/stats/functions/hclust) function requires a distance matrix as first argument and the `method` argument should be `"single"`.

`@sample_code`

```{r, eval = FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single


```


`@solution`

```{r, eval = FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single
run_single <- hclust(run_dist, method = "single")

```

`@sct`
```{r, eval=FALSE}
msg <- "Do not remove or overwrite the predefined variables."
test_object("run_record", undefined_msg = msg, incorrect_msg = msg)
test_object("run_record_sc", undefined_msg = msg, incorrect_msg = msg)

test_object("run_dist", 
            undefined_msg = "You forgot to calculate the distance matrix or assign it to <code>run_dist</code>", 
            incorrect_msg = "Did you use <code>run_record_sc</code> in <code>dist()</code>?")

test_object("run_single", 
            undefined_msg = "You forgot to make a single-linkage tree or assign it to <code>run_single</code>", 
            incorrect_msg = "Did you use <code>run_dist</code> and <code>method = \"single\"</code> in <code>hclust()</code>?")

```

***

```yaml
type: NormalExercise
xp: 20
key: 4ad96ef33e
```

`@instructions`

Cut the tree using [`cutree()`](http://www.rdocumentation.org/packages/stats/functions/cutree) at 5 clusters. Assign the result to `memb_single`.

`@hint`

Task 3 hint

`@sample_code`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single
run_single <- hclust(run_dist, method = "single")

# Apply cutree() to run_single: memb_single


```


`@solution`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single
run_single <- hclust(run_dist, method = "single")

# Apply cutree() to run_single: memb_single
memb_single <- cutree(run_single, k = 5)

```

`@sct`
```{r, eval=FALSE}
msg <- "Do not remove or overwrite the predefined variables."
test_object("run_record", undefined_msg = msg, incorrect_msg = msg)
test_object("run_record_sc", undefined_msg = msg, incorrect_msg = msg)

test_object("run_dist", 
            undefined_msg = "You forgot to calculate the distance matrix or assign it to <code>run_dist</code>", 
            incorrect_msg = "Did you use <code>run_record_sc</code> in <code>dist()</code>?")

test_object("run_single", 
            undefined_msg = "You forgot to make a single-linkage tree or assign it to <code>run_single</code>", 
            incorrect_msg = "Did you use <code>run_dist</code> and <code>method = \"single\"</code> in <code>hclust()</code>?")

test_correct({
  test_object("memb_single", 
              undefined_msg = "You forgot to assign your 5 highest clusters to <code>memb_single</code>!")
}, {
  test_function("cutree", "tree", 
                incorrect_msg = "In <code>cutree()</code>, did you pass the tree, <code>run_single</code>, correctly?")
  test_function("cutree", "k", 
                incorrect_msg = "In <code>cutree()</code>, did you cut the tree, <code>run_single</code>, at the 5 highest clusters?")
})

```

***

```yaml
type: NormalExercise
xp: 20
key: 4
```

`@instructions`

Make a dendrogram of `run_single` using [`plot()`](http://www.rdocumentation.org/packages/graphics/functions/plot). If you pass a hierarchical clustering object to [`plot()`](http://www.rdocumentation.org/packages/graphics/functions/plot), it will draw the dendrogram of this clustering.
Draw boxes around the 5 clusters using [`rect.hclust()`](http://www.rdocumentation.org/packages/stats/functions/rect.hclust). Set the `border` argument to `2:6`, for different colors.

`@hint`

Task 4 hint

`@sample_code`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single
run_single <- hclust(run_dist, method = "single")

# Apply cutree() to run_single: memb_single
memb_single <- cutree(run_single, k = 5)

# Apply plot() on run_single to draw the dendrogram

```

`@solution`

```{r, eval=FALSE}
# Apply dist() to run_record_sc: run_dist
run_dist <- dist(run_record_sc)

# Apply hclust() to run_dist: run_single
run_single <- hclust(run_dist, method = "single")

# Apply cutree() to run_single: memb_single
memb_single <- cutree(run_single, k = 5)

# Apply plot() on run_single to draw the dendrogram
plot(run_single)
rect.hclust(run_single, k = 5, border = 2:6)
```

`@sct`
```{r, eval=FALSE}
msg <- "Do not remove or overwrite the predefined variables."
test_object("run_record", undefined_msg = msg, incorrect_msg = msg)
test_object("run_record_sc", undefined_msg = msg, incorrect_msg = msg)

test_object("run_dist", 
            undefined_msg = "You forgot to calculate the distance matrix or assign it to <code>run_dist</code>", 
            incorrect_msg = "Did you use <code>run_record_sc</code> in <code>dist()</code>?")

test_object("run_single", 
            undefined_msg = "You forgot to make a single-linkage tree or assign it to <code>run_single</code>", 
            incorrect_msg = "Did you use <code>run_dist</code> and <code>method = \"single\"</code> in <code>hclust()</code>?")

test_correct({
  test_object("memb_single", 
              undefined_msg = "You forgot to assign your 5 highest clusters to <code>memb_single</code>!")
}, {
  test_function("cutree", "tree", 
                incorrect_msg = "In <code>cutree()</code>, did you pass the tree, <code>run_single</code>, correctly?")
  test_function("cutree", "k", 
                incorrect_msg = "In <code>cutree()</code>, did you cut the tree, <code>run_single</code>, at the 5 highest clusters?")
})

test_function("plot", "x", 
              not_called_msg = "Did you make a dendrogram of your tree, <code>run_complete</code>, using <code>plot()</code>?")

test_function("rect.hclust", args = c("tree", "k", "border"),
              not_called_msg = "Did you draw boxes around the five highest clusters using <code>rect.hclust()</code>?", 
              incorrect_msg = "When calling <code>rect.hclust()</code>, did you set your tree, <code>run_single</code>, as the first argument and <code>k = 5</code> as the second argument? Also don't forget to set <code>border</code> to <code>2:6</code>.")

test_error()
success_msg("Good job! However, it appears the two islands Samoa and Cook's Islands, who are not known for their sports performances, have both been placed in their own groups. Maybe, we're dealing with some chaining issues? Let's try a different linkage method in the next exercise!")
```
