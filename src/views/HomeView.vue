<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Peça já seu Churros!</h1>
      <ChurroForm />
    </div>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import ChurroForm from "../components/ChurroForm.vue";
export default {
  name: "Home",
  components: {
    Banner,
    ChurroForm,
  },
};
</script>
