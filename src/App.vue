<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <RouterLink to="/"
      ><img
        alt="Vue logo"
        class="logo"
        src="@/assets/chef.png"
        width="50"
        height="50"
    /></RouterLink>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/search">Search Food</RouterLink>
      <RouterLink to="/account">Account</RouterLink>
    </nav>
  </header>
  <RouterView />
</template>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
  background-color: var(--color3);
}

nav {
  display: flex;
  gap: 25px;
}
nav a {
  text-decoration: none;
  color: var(--color2);
  font-size: 1.2rem;
}
nav a.router-link-exact-active {
  font-weight: bold;
  color: var(--color1);
}
</style>
