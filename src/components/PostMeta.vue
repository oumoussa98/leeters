<template>
   <div class="post-meta">
      Posted {{ post.date }}.
      <template v-if="post.timeToRead">
        <strong>{{ post.timeToRead }} min read.</strong>
      </template>
      <span class="author">Created by
        <g-link target="_blank" :to='post.author_link'>
          {{ post.author }}
        </g-link>
      </span>
    </div>
</template>

<script>
export default {
  props: ['post']
}
</script>

<style lang="scss">
.post-meta {
  font-size: .8em;
  opacity: .8;
}
.post-meta .author {
  margin-left: 1em;
}
</style>