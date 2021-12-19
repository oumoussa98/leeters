---
title: Get_next_line
author: "@pride"
author_link: https://profile.intra.42.fr/users/habouiba
description: This project is to code a function that returns a
  newline-terminated line, read from a file descriptor. This project will help
  you learn static variables. Looping the get_next_line function
tags:
  - get_next_line
  - tips
  - algorithm
published: true
date: 2021-12-19T16:31:46.315Z
---
# Get Next Line

The goal of this project is to learn about **static variables** and improving
your **memory management** skills (allocating and freeing).

# Objectives

```c
char	*get_next_line(int fd);
```

## Requirements

* Static Variables

  		[Blog about static variables](https://www.c-programming-simple-steps.com/static-keyword-in-c.html)

  		[Video about static variables](https://www.youtube.com/watch?v=OngGUoENgWo)

* Dynamic Memory

  		[Blog about malloc](https://www.programiz.com/c-programming/c-dynamic-memory-allocation)
  	 
  		[Deep dive to malloc blog](https://danluu.com/malloc-tutorial/)
  	 
  		[Malloc video](https://www.youtube.com/watch?v=yFboyOwk2oM)
  	 
  		[Malloc video 2](https://www.youtube.com/watch?v=SuBch2MZpZM)
  	 
* File Descriptors

  		[File descriptor Blog](https://www.computerhope.com/jargon/f/file-descriptor.htm)
  	 
  		[File Descriptor Video](https://www.youtube.com/watch?v=BQJBe4IbsvQ)
  	 
  		[Advanced File descriptor Resource Video](https://www.youtube.com/watch?v=h5A1OQjuCqk&t=1s)
  	 

## Algorithm

* get a line

  * start with the content of the previous read data
  * read until new line or EOF
* make the content after new line in the static variable
* return the content from the start until new line
  	

## Tips

* be careful when using **ft_substr** and  **ft_strjoin** (memory leaks).
* you can implement the bonus first and copy it to the mandatory part.
* the static variable declaration : 

```c
static char		*backup[OPEN_MAX];
```