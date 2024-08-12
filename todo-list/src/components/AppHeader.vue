<template>
  <header>
    <h1>Todo<span>List</span></h1>
    <img src="../assets/emix-logo.png" alt="Emix logo" title="Emix logo" width="100px">
  </header>
</template>

<script>
export default {
  name: 'AppHeader'
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #006A6A;
  color: #fff;
  margin-bottom: 32px;
  padding: 8px 16px;
}

header h1 {
  margin: 0;
  text-transform: uppercase;
  font-weight: bolder;
}

header h1 span {
  font-weight: 100;
}
</style>