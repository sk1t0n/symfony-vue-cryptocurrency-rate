<template>
  <header>
    <b-navbar toggleable="md" type="dark" variant="dark" class="navbar">
      <b-navbar-brand href="/">{{ appName }}</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item v-for="link in links" :key="link.name" :href="link.path">{{ link.name }}</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>

<script>
export default {
  name: 'Header',

  props: {
    appName: {
      type: String,
      required: true
    }
  },

  data: () => ({
    links: [
      { name: 'Home', path: '/' },
      { name: 'About', path: '/about' },
    ]
  }),
};
</script>

<style lang="scss">
.navbar {
  padding: 1em;
}
</style>
