<template>
  <div class="wrapper">
    <h1>About</h1>
    <h3>Version 1.0.0</h3>
    <router-link to="/">Go back</router-link>
  </div>
</template>

<script>
export default {
  name: "About",
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
