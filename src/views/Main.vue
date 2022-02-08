<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="row">
        <div v-for="pokemon in pokemones" :key="pokemon.id" class="col-md-6">
          <Pokemon :pokemon="pokemon" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import pikachu from "../assets/pokemons/pikachu.png";
import raichu from "../assets/pokemons/raichu.png";
import raichushiny from "../assets/pokemons/raichushiny.png";
import charizard from "../assets/pokemons/charizard.png";

import Pokemon from "../components/Pokemon.vue";

export default {
  setup() {
    const pokemones = ref([
      {
        nombre: "Pikachu",
        color: "#90ee90",
        imagen: pikachu,
        evol: {
          evoluciona: true,
          imagen: raichu,
          variant: {
            normal: raichu,
            shiny: raichushiny,
          },
          nombre: "Raichu",
        },
        ataques: ["Trueno", "Chispa", "Agilidad", "Rayo"],
      },
      {
        nombre: "Charizard",
        color: "#f08080",
        imagen: charizard,
        evol: {
          evoluciona: false,
          imagen: charizard,
          variant: {
            normal: charizard,
            shiny: charizard,
          },
          nombre: "",
        },
        ataques: ["Llamarada", "Volar", "BolaFuego"],
      },
    ]);
    return {
      pokemones,
    };
  },
  components: {
    Pokemon,
  },
};
</script>

<style lang="scss" scoped></style>
