<template>
  <header>
    <img src="@/assets/img/netflix-logo.png" alt="logo netflix" />
  </header>
</template>

<script>
export default {
  name: "Header",
}; 
</script>

<style scoped lang="scss">
header {
  display: flex;
  align-items: center;
  background-color: #090909;
  width: 100%;
  padding: 10px 0;

  img {
      height: 45px;
      width: auto;
      margin-left: 40px;
  }
}
</style>