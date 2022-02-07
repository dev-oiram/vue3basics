<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="card">
        <img id="imgCard" v-bind:src="imagen" alt="Imagen" />
        <div class="card-body">
          <h5 class="card-title">{{ nombre }}</h5>
        </div>
        <div v-if="evol" class="card-footer">
          <i class="fas fa-angle-double-up"></i>
          <img v-bind:src="imagenEvol" alt="Imagen" />
          <p class="card-text">{{ nombreEvol }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import pikachu from "../assets/pokemons/pikachu.png";
import raichu from "../assets/pokemons/raichu.png";

export default {
  setup() {
    const nombre = ref("Pikachu");
    const imagen = pikachu;
    const evol = true;
    const imagenEvol = raichu;
    const nombreEvol = ref("Raichu");
    return {
      nombre,
      imagen,
      evol,
      imagenEvol,
      nombreEvol,
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
