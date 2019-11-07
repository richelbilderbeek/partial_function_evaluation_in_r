Partial Function Evaluation In R
========================================================
author:
date:
autosize: true

Goal
========================================================

 * Share a technique


Biological context
========================================================

![plot of chunk unnamed-chunk-1](partial_function_evaluation_in_r-figure/unnamed-chunk-1-1.png)

***

![plot of chunk unnamed-chunk-2](partial_function_evaluation_in_r-figure/unnamed-chunk-2-1.png)

Practice
========================================================

![](dt150421.gif)

Features
========================================================

 * Same number of taxa yes/no
 * Same sum of branch lengths yes/no
 * Same crown age yes/no
 * Speciation model: none, Yule, BD, etc.
 * Simulation method: random, maximum likelihood, etc..
 * Maximum number of simulation attempts

***

```
sim_twin_tree <- function(
  true_tree,
  ...
)
```

![](round_hole.jpg)

Simpler context
========================================================

 * R package: `greetr`


```r
library(greetr)
```

***


```r
params <- create_params(
  name = "Richel"
)

greet(params)
```


```
Hello Richel
```

Implementation
========================================================


```r
create_params <- function(
  name
) {
  list(
    name = name
  )
}
```

***


```r
greet <- function(params) {
  cat(
    paste("Hello", params$name)
  )
}
```

New use case: specify the greeting word
========================================================

![](phb.jpg)

***


```r
params <- create_params(
  greeting = "Howdy",
  name = "Richel"
)
greet(params)
```


```
Howdy Richel
```

New use case: specify the greeting word
========================================================


```r
create_params <- function(
  name,
  greeting = "Hello"
) {
  list(
    name = name,
    greeting = greeting
  )
}
```

***


```r
greet <- function(params) {
  cat(
    paste(
      params$greeting,
      params$name
    )
  )
}
```




New use case: greeting word depends on the language
========================================================

![](phb.jpg)

***


```r
params <- create_params(
  language = "Dutch",
  name = "Richel"
)
greet(params)
```


```
Hallo Richel
```

New use case: greeting word depends on the language
========================================================


```r
params <- create_params(
  name,
  greeting = "Hello",
  language = NA
) {
  list(
    # ...
    language = language
  )
}
```

***


```r
greet <- function(params) {
  if (
    !is.na(params$language)
  ) {
    # Greet in language
  } else {
    # Greet with greeting
  }
}
```

 * Code smell: not all parameters are used in all contexts

New use case: greeting word depends on the weather
========================================================

![](phb.jpg)

***


```r
params <- create_params(
  weather = "sunny",
  temperature = 25,
  name = "Richel"
)
greet(params)
```


```
Hello Richel :sunglasses: :cocktail:
```

New use case: greeting word depends on the weather
========================================================


```r
params <- create_params(
  # ...
  weather = NA,
  temperature = NA,
) {
  list(
    # ...
    weather = weather,
    temperature =
      temperature
  )
}
```

 * Code smell: if one parameter is used, so must another

***


```r
greet <- function(params) {
  if (!
      is.na(params$weather)
  ) {
    # Must specify both
    testit::assert(
      !is.na(
        params$temperature
      )
    )
    # ...
  }
  # ...
}
```

How to make this fit?
========================================================

![](round_hole.jpg)
