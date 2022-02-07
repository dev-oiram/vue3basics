<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="card">
        <img id="imgCard" v-bind:src="imagen" alt="Imagen" />
        <div class="card-body">
          <h5 class="card-title">{{ nombre }}</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const nombre = ref("Pikachu");
    const imagen = require("../assets/pokemons/pikachu.png");
    return {
      nombre,
      imagen,
    };
  },
};
</script>

<style lang="scss" scoped>
.card {
  width: 10rem;
}
#imgCard {
  background-color: lightblue;
}
</style>
