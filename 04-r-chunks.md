# The R chunks

In [Markdown section](#vanilla-markdown) I've showed you how to start new Rmarkdown document in RStudio, but lets briefly recap how we do that.

```
File
 └── New File
        └── R Markdown

title = "Learning Rmarkdown"
author = "Me"
```

- select document type **HTML**
- to build (compile) the document press `knitr` button or `ctrl+alt+k`
- to save as `.Rmd` file

## Why Rmarkdown again?

The reason that we are using [Rmarkdown](https://rmarkdown.rstudio.com/) is because there is no alternative, really? Really.

Irrespective of the programming language used we'll have to write code and one way or anther you'll be writing notes and comments that will go along with that chunk of code. It makes sense to keep those comments (text) close to the code, inside the same file ideally. That idea isn't novel I and hope that all of you comment your code well. Common commenting characters:

- `#`
- `/*  */`
- `//`

But the comments are never seem in the output and can only be accessed by one looking into the source. But wouldn't it be nice if we can see the code, the output and the comments together?

This type approach is supper common and supper useful when you working with some data and you are trying to convey some message to a different person (people) by means of examples and/or illustration of the analysis flow. Not only one can read your notes about the analysis, that are placed exactly next the piece of code or data by the way, but one can also see the code that one wrote for that analysis.

## Embedding R code

RStudio is pretty good it templates our Rmd file a bit. Lets delete all the text past these lines.


````
---
title: 'Learning Rmarkdown'
author: 'Kirill'
date: '21/06/2019'
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
````

I'm going to explain `knitr::opts_chunk` bit shortly, but for now let's skip that part and move on to embedding R code into the document.

Any R code has to be inside "special" block - chunk, this one


````
```{r}

```
````

Little `r` there specifies the "engine", which interpreter to use to "understand" the text inside that chunk. Here we are saying use `R` engine (language) to evaluate the code. The [list of languages](https://bookdown.org/yihui/rmarkdown/language-engines.html) is rather long actually, but for now let's only focus on R language, otherwise it becomes even harder to explain Rmarkdown. As I've hinted in the introduction section is so ubiquitous that you can't avoid it anymore.

Let's write our first bit of R code inside the Rmarkdown document. First we need to start a new R chunk, which can be done in either of three ways:

- simply type it out
- press insert button at the top of the window
- `ctrl+alt+i`

Let's start with a simple `print()` statement and print `Hello world, I'm learning Rmarkdown !` string, except we are going to split it between two variable



````
```{r}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```
````

Note that each chunk can be run independently in the console by pressing `ctrl^enter` or little green arrow.

Each code chunk is highly customisable via [chunk options](https://bookdown.org/yihui/rmarkdown/r-code.html). We are going to learn a few today, but we won't be able to cover all of them. You probably never going to use some of them, but as long as you know what to look for you'll be able to search for then on the internet. Note that all chunk options have a default value, by not specifying the options you are simply using the default option.

General layout of any chunk is


````
```
{r chunk_name, options}
```
````

Note a couple of things, there isn't a comma between `r` and `chunk_name`. Not sure why this is..
Also note that `chunk_name` is optional, you can skip it, as we have in earlier examples. Naming chunks is good idea to conceptually label the chunk as to what it does, but also we you are going to build more sophisticated documents you'll be able to selectively include chunks by refer to them by the chunk name.

Lets start off with these three chunk options:

- `echo` show what has been typed in i.e show the code
- `eval` evaluate or execute that code
- `results` hide resulting output

These allow us fine level control over the final document. Think about who are generating the document for and what type of information you need to share. Sometimes we might want to show the code, but not execute it and other times we might just want to execute it and share the results, e.g plot, without actually showing the code.

Let's start with `echo = TRUE` and `eval = TRUE`.


````
```{r echo = T, eval = T}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```
````


```r
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```

```
## [1] "Hello world, Im learning Rmarkdown !"
```

Now let's turn `echo` off, `echo=FALSE`.


````
```{r echo = F}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```
````


```
## [1] "Hello world, Im learning Rmarkdown !"
```

Okay, we don't see our original `print()` statement. And now let's pass `eval=FALSE` options instead


````
```{r eval = F}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```
````


```r
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```

Now we see the code, but not the output. The difference between `echo` and `results` is subtle, at least in my head. Let's consider the following example.



````
```{r echo = T, eval = F, results = 'asis'}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```

```{r}
ab
```
````


```r
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```


```r
ab
```

```
## [1] "Hello world, Im learning Rmarkdown !"
```

Let's turn `results = 'hide'`


````
```{r echo = T, eval = F, results = 'hide'}
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```
```{r}
ab
```
````


```r
a <- 'Hello world,'
b <- 'Im learning Rmarkdown !'
ab <- paste(a, b)
print(ab)
```

[1] "Hello world, Im learning Rmarkdown !"


```r
ab
```

```
## [1] "Hello world, Im learning Rmarkdown !"
```

And now we only see `print()` statement and no output.


## Challenge: code chunks {.exercise}

> 3 minutes

<details>
  <summary>
    1. Go through all of your code so far and give each chunk a name
  </summary>

  
  ````
  ```
  {r chunk_name, options}
  ```
  ````
</details>

##  References

[Here is nice cheatsheet](http://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf) that has comprehensive cover of all the options you can pass in.