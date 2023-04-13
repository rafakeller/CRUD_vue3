<template>
  <div id="main-banner">
    <h1>Faça seu Churros!</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/public/img/burger.jpg");
  background-position: 0 -250px;
  background-size: cover;
  height: 600px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
#main-banner h1 {
  color: var(--bege);
  text-align: center;
  font-size: 60px;
  background-color: var(--azul-escuro);
  padding: 20px 40px;
  font-weight: 500;
}
</style>
