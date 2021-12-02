---
title: A post with a cover image
author: Sra9ziit
author_link: https://profile.intra.42.fr/users/aeddaoud
description: Markdown is intended to be as easy-to-read and easy-to-write as is
  feasible. Readability, however, is emphasized above all else. A
  Markdown-formatted document should be publishable as-is, as plain text,
  without looking like it's been marked up with tags or formatting instructions.
tags:
  - Markdown
  - Cover Image
published: true
date: 2019-01-07
---
![]('./images'/download.png)

```js
<script setup>
  // this is a comment by sra9ziit
  import { ref } from "vue";
  import InfiniteLoading from "v3-infinite-loading";
  import "v3-infinite-loading/lib/style.css";

  let comments = ref([]);
  let page = 1;
  const load = async $state => {
    console.log("loading...");

    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/comments?_limit=10&_page=" + page
      );
      const json = await response.json();
      if (json.length < 10) $state.complete();
      else {
        comments.value.push(...json);
        $state.loaded();
      }
      page++;
    } catch (error) {
      $state.error();
    }
  };
</script>
```

```html
<template>
  <div class="result" v-for="comment in comments" :key="comment.id">
    <div>{{ comment.email }}</div>
    <div>{{ comment.id }}</div>
  </div>
  <InfiniteLoading :comments="comments" @infinite="load" />
</template>
```