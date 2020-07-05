<template>
  <header class="header">
    <img alt="Vue logo" src="../../assets/logo.png" class="logo" />

    <h1>Todo List</h1>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  background-color: lightblue;
  color: var(--main-grey);
  padding: 0.5rem;
  text-align: center;
}
.logo {
  max-height: 10vh;
  width: auto;
}
</style>
