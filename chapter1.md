---
title       : SCT quiz
description : 
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:NormalExercise lang:r xp:100 skills:1 key:31ea872ce2
## Simple tests (1)

#### pass 1

```
library('zoo')

x <- zoo(1:3)

print(x)
```

#### pass 2

```
library(zoo)

x <- y <- zoo(1:3)

print(y)
```

#### fail 1 - "x is not correct"

```
library(zoo)

x = c(1,2,3)

print(x)
```

#### fail 2 - "x is undefined"

```
library(zoo)
```

#### fail 3 - "Expected same output as `zoo(1:3)`"

```
library(zoo)

x <- zoo(1:3)
```


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
library(zoo)

x <- zoo(1:3)

print(x)
```

*** =solution
```{r}
library(zoo)

x <- zoo(1:3)

print(x)
```

*** =sct
```{r}
test_library_function("zoo")
test_correct({
    test_object("x", incorrect_msg = "Did you correctly define `x`? Use the `zoo()` function.", undefined_msg = "Did you define `x`?")
    }, {
    test_function("zoo", args = "x", incorrect_msg = "Did you pass `1:3` to the `zoo()` function?", not_called_msg = "Have you called `zoo()` to define `x`?")
})
test_output_contains("print(x)")
test_error()
success_msg("Nice!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:86f183628a
## Simple tests (2)


#### pass 1

```
f("blue")
```

#### pass 2

```
f( "b" )
```

#### pass 3

```
f('b')
```

#### pass 4
```
(f("b"))
```

#### fail 1 - "should call f('blue') or f('b')"

```
f("blueberry")
```

#### fail 2 - "should cal f('blue') or f('b')"

```
pf("blue")
```


*** =pre_exercise_code
```{r}
f <- function(x) NULL
pf <- function(x) NULL
```

*** =sample_code
```{r}
f("b")
```

*** =solution
```{r}
f("b")
```

*** =sct
```{r}
# Use only a check_code SCT
test_correct({
    test_function("f", not_called_msg = "should cal f('blue') or f('b')")
    }, {
    test_or(test_student_typed("f('b')", not_typed_msg = "should call f('blue') or f('b')"),
            test_student_typed("f('blue')", not_typed_msg = "should call f('blue') or f('b')"),
            incorrect_msg = "should call f('blue') or f('b')")
}) 

# I'm not sure how to use regex inside test_student_typed() for it to catch incorrect usage of pf()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:69cbf4cfc4
## Control Tests (1)

#### pass

```
for (jj in 1:10) if (jj > 1) jj else 0
```

#### fail 1 - "bad cond test"

```
for (jj in 1) if (jj > 1) jj else 0
```

#### fail 2 - "no inner if"

```
for (ii in 1:10) ii
```

#### fail 3 - "bad if cond"

```
for (ii in 1:10) if (ii > 1000) ii else 0
```

#### fail 4 - "no else cond"

```
for (ii in 1:10) if (ii > 1) ii
```

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
for (ii in 1:10) if (ii > 1) ii else 0
```

*** =solution
```{r}
for (ii in 1:10) if (ii > 1) ii else 0
```

*** =sct
```{r}
test_for_loop(1,
              cond_test = test_student_typed("in 1:10", not_typed_msg = "bad cond test"),
              expr_test = test_if_else(1,
                                       if_cond_test = test_student_typed("> 1", not_typed_msg = "bad if cond"), # I know this doesn't filter > 1000 but adding the $ metacharacter at the end returns an error. Having the same issue as last exercise.
                                       not_found_msg = "no inner if",
                                       else_expr_test = test_student_typed("0", not_typed_msg = "bad else expr"),
                                       missing_else_msg = "no else cond"))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:72a629a74f
## Data Objects

#### pass

```
d <- transform(d, ttl = x + y)
```

#### fail 1 - "d is undefined"

```
rm('d')
```

#### fail 2 - "bad value for ttl"

```
d$ttl <- d$x
```

#### fail 3 - "missing col y"

```
d$ttl <- d$x + d$y
d$y <- NULL
```

*** =pre_exercise_code
```{r}
d <- data.frame(x=1:10, y=11:20)
```

*** =sample_code
```{r}
d$ttl <- d$x + d$y
```

*** =solution
```{r}
d$ttl <- d$x + d$y
```

*** =sct
```{r}
# The erorr msg for fail 3 isn't what I expect but it works for this purpose I guess
test_data_frame("d", undefined_msg = "`d` is undefined", columns = c("ttl", "y"), incorrect_msg = c("bad value for `ttl`", "missing col `y`"))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:631d01c691
## Function Definition

#### pass 1

```
f <- function(x, y, z=1) sum(x + y, z)
```

#### fail 1 - "missing 3rd arg"

```
f <- function(a, b) sum(a + b)
```

#### fail 2 - "no + operator"

```
f <- function(a, b, c=1) sum(a,b,c)
```

#### fail 3 - "no sum call"

```
f <- function(a, b, c=1) a + b + c
```

*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
f <- function(a, b, c=1) sum(a + b, c)
```

*** =solution
```{r}
f <- function(a, b, c=1) sum(a + b, c)
```

*** =sct
```{r}
test_function_definition("f",
                         function_test = {
                           test_expression_result("f(1, 2)")
                           test_expression_error("f('n', 1)")
                         },
                         incorrect_number_arguments_msg = "missing 3rd arg",
                         body_test = {
                           test_student_typed("+", not_typed_msg = "no + operator")
                           test_function("sum", not_called_msg = "no sum call") # This doesn't work as I expected
                         })
                           
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7839a0890c
## Function Call

#### pass 1 

```
lm(d$x ~ d$y)
```

#### pass 2

```
with(d, lm(x ~ y))
```

*** =pre_exercise_code
```{r}
d <- data.frame(x = 1:10, y = 11:20)
```

*** =sample_code
```{r}
lm(x ~ y, data=d)
```

*** =solution
```{r}
lm(x ~ y, data=d)
```

*** =sct
```{r}
# No idea how to test this one effectively...
test_function("lm")
test_student_typed("x")
test_student_typed("~")
test_student_typed("d")
test_student_typed("y")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f033369188
## Function Call (2)

#### pass 1 - 

```
lapply(df, function(col) sum(col))
```

#### fail 1 - "missing first pos arg"

```
lapply(FUN=sum)
```

#### fail 2 - "incorrect first pos arg"

```
lapply(sum)
```

#### fail 3 - "missing second pos arg"

```
lapply(df)
```


*** =pre_exercise_code
```{r}
df <- data.frame(a = 1:10, b = 11:20)
```

*** =sample_code
```{r}
lapply(df, sum)
```

*** =solution
```{r}
lapply(df, sum)
```

*** =sct
```{r}
# I don't understand how R automatically matches a variable to an argument
test_function("lapply", c("X","FUN"), eval = NA, args_not_specified_msg = c("missing first pos arg", "missing second pos arg"), incorrect_msg = c("incorrect first pos arg", "incorrect second pos arg"))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:2564475b6e
## Logic Test

#### pass - 

```
x <- mean(1:3)
lkjsdf
```

#### fail 1 - "error in code"

```
x <- men(1:3)
```

#### fail 2  - "undefined x"

```
```

#### fail 3 - "did you call mean?"

```
x <- 2
```


*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
x <- mean(1:3)
```

*** =solution
```{r}
x <- mean(1:3)
```

*** =sct
```{r}
test_correct({
    test_expression_result("x")
    test_function("mean", "x")
    }, {
    test_error()
    test_object("x")
    })
```

--- type:NormalExercise lang:r xp:100 skills:1 key:f02f67218b
## Backend Trouble

Use a testwhat function in the pre\_exercise\_code, to allow the solution to pass.

*** =pre_exercise_code
```{r}
#? :(
```

*** =sample_code
```{r}
f <- function(a) stopifnot(a > 5)
f(3)
```

*** =solution
```{r}
f <- function(a) stopifnot(a > 5)
f(3)
```

*** =sct
```{r}
# :(
```

