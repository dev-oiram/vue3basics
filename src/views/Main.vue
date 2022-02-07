<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="card">
        <img id="imgCard" v-bind:src="pokemon.imagen" alt="Imagen" />
        <div class="card-body">
          <h5 class="card-title">{{ pokemon.nombre }}</h5>
          <button @click="verEvolucion" class="btn btn-primary">Evolución</button>
        </div>
        <div v-if="verEvol" class="card-footer">
          <i class="fas fa-angle-double-up"></i>
          <img v-bind:src="pokemon.evol.imagen" alt="Imagen" />
          <p class="card-text">{{ pokemon.evol.nombre }}</p>
          <span @mouseover="cambio(pokemon.evol.variant.normal)">
            <i class="fas fa-lightbulb m-2"></i>
          </span>
          <span @mouseover="cambio(pokemon.evol.variant.shiny)">
            <i class="far fa-lightbulb m-2"></i>
          </span>
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
import { ref, reactive } from "vue";
import pikachu from "../assets/pokemons/pikachu.png";
import raichu from "../assets/pokemons/raichu.png";
import raichushiny from "../assets/pokemons/raichushiny.png";

export default {
  setup() {
    const verEvol = ref(false);
    const pokemon = reactive({
      nombre: "Pikachu",
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
    });
    const verEvolucion = () => {
      verEvol.value = !verEvol.value;
    };
    const cambio = (valor) => {
      pokemon.evol.imagen = valor;
    };
    return {
      pokemon,
      verEvol,
      verEvolucion,
      cambio,
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
