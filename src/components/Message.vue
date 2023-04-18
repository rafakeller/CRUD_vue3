<template>
  <div class="message-container">
    <p>{{msg}}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container{
  color:var(--azul-escuro);
  background-color:var(--amarelo);
  border: 2px solid var(--branco);
  border-radius:5px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}

</style>
