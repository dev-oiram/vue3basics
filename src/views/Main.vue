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
            <span><i class="fas fa-shopping-cart"></i></span>({{ carrito.length }})
            Carrito
          </h5>
          <hr />
          <div v-for="(producto, index) in carrito" :key="index">
            <Producto :pokemon="producto" />
            <span style="color: red" @click="quitarCarrito(index)">Quitar</span>
            <hr />
          </div>
        </div>
      </div>
      <div>
        <h5>Reseñas</h5>
        <hr />
        <div class="row">
          <div class="col-md-4">
            <form @submit.prevent="agregarReview">
              <div class="mb-1">
                <label for="nombre" class="form-label">Nombre:</label>
                <input
                  v-model="review.nombre"
                  type="text"
                  class="form-control"
                  id="nombre"
                  required
                />
              </div>
              <div class="mb-1">
                <label for="res" class="form-label">Reseña:</label>
                <textarea
                  v-model="review.review"
                  class="form-control"
                  id="res"
                  row="4"
                  required
                />
              </div>
              <button type="submit" class="btn btn-success">Agregar</button>
            </form>
          </div>
          <div class="col-md-8 text-center">
            <div
              v-for="re in reviews"
              :key="re.id"
              class="card text-white bg-success mb-2"
            >
              <div class="card-header">
                <h5>{{ re.nombre }}</h5>
              </div>
              <div class="card-body">
                <p>{{ re.review }}</p>
              </div>
            </div>
          </div>
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
    // Reseña
    let review = reactive({
      nombre: "",
      review: "",
    });
    let reviews = ref([]);
    const agregarReview = () => {
      let obj = {
        nombre: review.nombre,
        review: review.review,
      };
      reviews.value.push(obj);
      review.nombre = "";
      review.review = "";
    };
    return {
      pokemones,
      carrito,
      agregarCarrito,
      quitarCarrito,
      review,
      reviews,
      agregarReview,
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
.card {
  width: 30rem;
}
</style>
