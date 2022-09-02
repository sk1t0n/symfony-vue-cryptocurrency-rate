<template>
  <footer class="bg-dark">
    Copyright &copy; {{ year }} &nbsp;|&nbsp; All rights reserved. &nbsp;|&nbsp; {{ author }}
  </footer>
</template>

<script>
export default {
  name: 'Footer',

  data: () => ({
    year: new Date().getFullYear(),
    author: 'Anton Grabovsky'
  }),
};
</script>

<style lang="scss" scoped>
footer {
  width: 100%;
  height: 60px;
  line-height: 60px;
  text-align: center;
  color: #fff;
}
</style>
