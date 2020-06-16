<template>
  <section>
    <h1>Compre ou Venda</h1>
    <ProdutosBuscar />
    <ProdutosLista />
  </section>
</template>

<script>
import ProdutosBuscar from "@/components/ProdutosBuscar.vue";
import ProdutosLista from "@/components/ProdutosLista.vue";

export default {
  name: "Home",
  components: {
    ProdutosBuscar,
    ProdutosLista
  }
};
</script>

<style lang="scss" scoped>
h1 {
  @include font;
  font-size: 2rem;
  margin-top: 40px;
  color: $second_color;
  text-align: center;
}
</style>
