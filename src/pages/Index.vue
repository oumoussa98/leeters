<template>
  <Layout>
    <!-- List posts -->
    <div class="posts">
      <PostCard v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node"/>
    </div>
    <div class="pager">
      <Pager class="pager__component" :info="$page.posts.pageInfo"/>
    </div>
  </Layout>
</template>

<page-query>
query($page: Int) {
  posts: allPost(filter: { published: { eq: true }}, perPage: 1, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        path
        tags {
          id
          title
          path
        }
      }
    }
  }
}
</page-query>

<script>
import PostCard from '~/components/PostCard.vue'
import { Pager } from 'gridsome'

export default {
  components: {
    PostCard,
    Pager
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<style>
.pager {
  margin: 0 auto;
  display: flex;
  justify-content: center;  
}
.pager__component {
  display: flex;
  align-items: center;
  gap: 1rem;
}
.pager__component a {
  text-decoration: none;

}
</style>
