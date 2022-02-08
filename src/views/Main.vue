<template>
  <div>
    <h3>Main</h3>
    <div class="container">
      <div class="row">
        <div class="col-md-8">
          <div class="row">
            <div v-for="pokemon in pokemones" :key="pokemon.id" class="col-md-6">
              <Pokemon :pokemon="pokemon" @agregaCarrito="agregarCarrito" />
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <h5>
            <span><i class="fas fa-shopping-cart"></i></span>({{ carrito.length }})Carrito
          </h5>
          <hr />
          <div v-for="(producto, index) in carrito" :key="index">
            <Producto :pokemon="producto" />
            <span style="color: red" @click="quitarCarrito(index)">Quitar</span>
            <hr />
          </div>
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
import Producto from "../components/Producto.vue";

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
    // Carrito
    let carrito = ref([]);
    const agregarCarrito = (pokemon) => {
      carrito.value.push(pokemon);
    };
    const quitarCarrito = (id) => {
      carrito.value.splice(id, 1);
      const car = carrito.value;
      carrito.value = [];
      // Solucion Temporal
      const timer = setTimeout(() => {
        carrito.value = car;
      }, 10);
    };
    return {
      pokemones,
      carrito,
      agregarCarrito,
      quitarCarrito,
    };
  },
  components: {
    Pokemon,
    Producto,
  },
};
</script>

<style lang="scss" scoped>
span {
  cursor: pointer;
}
</style>
