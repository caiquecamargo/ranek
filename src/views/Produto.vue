<template>
  <section v-if="produto" class="produto">
    <ul class="fotos">
      <li v-for="(foto, index) in produto.fotos" :key="index">
        <img :src="foto.src" :alt="foto.titulo" />
      </li>
    </ul>
    <div class="info">
      <h1 class="titulo">{{produto.nome}}</h1>
      <p class="preco">{{produto.preco | numeroPreco}}</p>
      <p class="descricao">{{produto.descricao}}</p>
      <transition-group mode="out-in" v-if="produto.vendido === 'false'">
        <button class="btn" v-if="!finalizar" @click="finalizar = true" key="button">Comprar</button>
        <FinalizarCompra v-else :produto="produto" key="form" />
      </transition-group>
      <button class="btn" v-else disabled>Produto Vendido</button>
    </div>
  </section>
</template>

<script>
import { api } from "@/services.js";
import FinalizarCompra from "@/components/FinalizarCompra.vue";

export default {
  name: "Produto",
  props: ["id"],
  components: {
    FinalizarCompra
  },
  data() {
    return {
      produto: null,
      finalizar: false
    };
  },
  methods: {
    getProduto() {
      api.get(`/produto/${this.id}`).then(response => {
        this.produto = response.data;
      });
    }
  },
  created() {
    this.getProduto();
  }
};
</script>

<style lang="scss" scoped>
.titulo {
  font-size: 1.8rem;
  font-weight: bold;
}
.produto {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  max-width: 900px;
  padding: 60px 20px;
  margin: 0 auto;
}

.preco {
  color: $third_color;
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 40px;
}

.descricao {
  font-size: 1.2rem;
}

.btn {
  @include button;
  margin-top: 60px;
}
</style>