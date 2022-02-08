<template>
  <div>
    <div v-if="producto" class="row">
      <div class="col-md-4">
        <img class="img-fluid" :src="producto.imagen" />
      </div>
      <div class="col-md-8">
        <h5>{{ producto.nombre }}</h5>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";

export default {
  props: {
    pokemon: Object,
  },
  setup(props) {
    let producto = reactive({});
    const setProducto = () => {
      Object.assign(producto, props.pokemon);
    };
    onMounted(() => {
      setProducto();
    });
    return {
      producto,
    };
  },
};
</script>

<style lang="scss" scoped>
img {
  max-width: 50px;
  max-height: 50px;
}
</style>
