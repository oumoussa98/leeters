<template>
	<g-link class="logo" to="/">
	  &larr;
	  <span class="logo__text">
	     {{ $static.metadata.siteName }}
	  </span>
	</g-link>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Sacramento&display=swap");

.logo {
  text-decoration: none;
}

.logo__text {
  font-size: 30px;
  color: var(--body-color);
  font-family: "Sacramento", cursive;
  text-align: center;
}


</style>
