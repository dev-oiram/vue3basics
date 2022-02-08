<template>
  <div>
    <div class="card">
      <img
        v-bind:src="pokemon.imagen"
        alt="Imagen"
        :style="{ backgroundColor: pokemon.color }"
      />
      <div class="card-body">
        <h5 class="card-title">{{ pokemon.nombre }}</h5>
        <button
          @click="verEvolucion"
          class="btn"
          :class="[!pokemon.evol.evoluciona ? 'btn-secondary' : 'btn-primary']"
          :disabled="!pokemon.evol.evoluciona"
        >
          Evolución
        </button>
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
</template>

<script>
import { ref, reactive, computed, onMounted } from "vue";

export default {
  props: {
    pokemon: Object,
  },
  setup(props) {
    const verEvol = ref(false);
    let pokemon = reactive({});
    const setPokemon = () => {
      Object.assign(pokemon, props.pokemon);
    };
    const verEvolucion = () => {
      verEvol.value = !verEvol.value;
    };
    const cambio = (valor) => {
      pokemon.evol.imagen = valor;
    };
    const evolDetalle = computed(() => {
      return pokemon.nombre + " > " + pokemon.evol.nombre;
    });
    onMounted(() => {
      setPokemon();
    });
    return {
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
