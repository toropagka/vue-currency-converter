<template>
  <div class="container">
    <router-link to="/">список валют</router-link>
    <router-link to="/currencies_list">конвертер валют</router-link>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  text-decoration: none;
  height: 100px;
  margin: 0px auto;
  background-color: rgb(38, 119, 92);
}
a {
  width: 300px;
  height: 40px;
  margin: 0 auto;
  text-decoration: none;
  font-size: 2rem;
  color: white;
}
a:hover {
  border: 2px dotted rgb(226, 214, 160);
  transition: all 0.1s linear;
}
</style>
