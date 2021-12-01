<template>
  <div id="app">

    <header class="header">
      <div class="header__left">
        <Logo v-if="showLogo" /> 
      </div>
      <div>
        <Search />
      </div>
      <div class="header__right">        
        <ToggleTheme />
      </div>
    </header>

    <main class="main">
      <slot/>
    </main>

    <!-- <footer class="footer">
      <span class="footer__copyright">Made with ❤️</span>
      <span class="footer__links">by <a href="//oumoussa.tech"> oumoussa </a></span>
    </footer> -->

  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import ToggleTheme from '~/components/ToggleTheme.vue'
import Search from '~/components/Search.vue'


export default {
  props: {
    showLogo: { default: true }
  },
  components: {
    Logo,
    ToggleTheme,
    Search
  },
}
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: var(--header-height);
  padding: 0 calc(var(--space) / 2);
  top:0;
  z-index: 10;
  max-width: 1400px;
  margin: 0 auto;

  &__left,
  &__right {
    display: flex;
    align-items: center;
  }

  @media screen and (min-width: 1300px) {
    //Make header sticky for large screens
    width: 100%;
  }
}

.main {
  margin: 20px auto 0 auto;
  padding: 1.5vw 15px 0;
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: calc(var(--space) / 2);
  text-align: center;
  font-size: .8em;

  > span {
    margin: 0 .35em;
  }

  a {
    color: currentColor;
  }
}
</style>
