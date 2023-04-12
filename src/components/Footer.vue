<template>
  <div id="footer">
    <p>Make Your Churros &copy; 2023</p>
  </div>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
#footer{
  height: 200px;
  background-color: var(--azul-escuro);
  border-top: 2px solid var(--preto);
  color: var(--laranja);
  display: flex;
  align-items: center;
  justify-content: center;
  bottom: 0;
  width: 100%;
  margin-top: 138px;
}
</style>
