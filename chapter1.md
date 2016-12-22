---
title       : Insert the chapter title here
description : Insert the chapter description here
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

#### fail 1 - "x is not class 'zoo'"

```
library(zoo)

x = c(1,2,3)

print(x)
```

#### fail 3 - "x is undefined"

```
library(zoo)
```

#### fail 4 - "Expected [1,2,3] in your output"

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

#### fail 1 - "should call f('blue') or f('b')

```
f("blueberry")
```

#### fail 2 - "should cal f('blue') or f('b')"

```
pf("blue")
```


*** =pre_exercise_code
```{r}
f <- function(x)
pf <- function(x)
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
```
