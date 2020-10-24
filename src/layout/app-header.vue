<template>
  <header class="header">
    <router-link class="header__logo" :to="{name: 'gallery'}"><img src="/img/gallery.jpg" height="30" width="30"/>Photo Gallery</router-link>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
};
</script>

<style lang="scss" scoped>
.header {
  padding: 15px;
  background-color: #66cc00;
  border-color: #66cc00;
  position: sticky;
  top: 0;
  z-index: 1;
  text-align: center;
}

.header__logo img {
  margin: 5px 5px;
  vertical-align: middle;
}
.header__logo {
  color: white;
  text-decoration: none;
  font-size: 1.5em;
}
</style>
