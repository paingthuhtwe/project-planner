<template>
  <nav class="text-center my-[3em]">
    <router-link class="text-xl px-3" to="/">Projects</router-link> |
    <router-link class="text-xl px-3" :to="{ name: 'AddProject' }"
      >Add New Project</router-link
    >
  </nav>
</template>

<script scoped>
export default {};
</script>

<style>
nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>