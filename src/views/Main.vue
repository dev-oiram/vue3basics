<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="card">
        <img id="imgCard" v-bind:src="pokemon.imagen" alt="Imagen" />
        <div class="card-body">
          <h5 class="card-title">{{ pokemon.nombre }}</h5>
        </div>
        <div v-if="pokemon.evol.evoluciona" class="card-footer">
          <i class="fas fa-angle-double-up"></i>
          <img v-bind:src="pokemon.evol.imagen" alt="Imagen" />
          <p class="card-text">{{ pokemon.evol.nombre }}</p>
        </div>
        <div class="card-footer">
          <h5>Ataques:</h5>
          <ul>
            <li v-for="ataque in pokemon.ataques" :key="ataque.id">
              {{ ataque }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
import pikachu from "../assets/pokemons/pikachu.png";
import raichu from "../assets/pokemons/raichu.png";

export default {
  setup() {
    const pokemon = reactive({
      nombre: "Pikachu",
      imagen: pikachu,
      evol: {
        evoluciona: true,
        imagen: raichu,
        nombre: "Raichu",
      },
      ataques: ["Trueno", "Chispa", "Agilidad", "Rayo"],
    });
    return {
      pokemon,
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
