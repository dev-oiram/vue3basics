<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="card">
        <img v-bind:src="pokemon.imagen" alt="Imagen" :style="{ backgroundColor: pokemon.color }" />
        <div class="card-body">
          <h5 class="card-title">{{ pokemon.nombre }}</h5>
          <button @click="verEvolucion" class="btn" :class="[!pokemon.evol.evoluciona ? 'btn-secondary' : 'btn-primary']" :disabled="!pokemon.evol.evoluciona">Evolución</button>
        </div>
        <div v-if="verEvol" class="card-footer">
          <i class="fas fa-angle-double-up"></i>
          <img v-bind:src="pokemon.evol.imagen" alt="Imagen" />
          <p class="card-text">{{ evolDetalle }}</p>
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
import { ref, reactive, computed } from "vue";
import pikachu from "../assets/pokemons/pikachu.png";
import raichu from "../assets/pokemons/raichu.png";
import raichushiny from "../assets/pokemons/raichushiny.png";

export default {
  setup() {
    const verEvol = ref(false);
    const pokemon = reactive({
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
    });
    const verEvolucion = () => {
      verEvol.value = !verEvol.value;
    };
    const cambio = (valor) => {
      pokemon.evol.imagen = valor;
    };
    const evolDetalle = computed(() => {
      return pokemon.nombre + ' > ' + pokemon.evol.nombre
    })
    return {
      pokemon,
      verEvol,
      verEvolucion,
      cambio,
      evolDetalle,
    };
  },
};
</script>

<style lang="scss" scoped>
.card {
  width: 10rem;
}
</style>
