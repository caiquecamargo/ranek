<template>
  <section class="produtos-container">
    <transition mode="out-in">
      <div v-if="produtos && produtos.length" class="produtos" key="produtos">
        <div class="produto" v-for="(produto, index) in produtos" :key="produto.id+index">
          <router-link :to="{name: 'produto', params: {id: produto.id}}">
            <img v-if="produto.fotos" :src="produto.fotos[0].src" :alt="produto.fotos[0].nome" />
            <p class="preco">{{produto.preco | numeroPreco}}</p>
            <h2 class="titulo">{{produto.nome}}</h2>
            <p class="descricao">{{produto.descricao}}</p>
          </router-link>
        </div>
        <ProdutosPaginar :produtosTotal="produtosTotal" :produtosPorPagina="produtosPorPagina" />
      </div>
      <div v-else-if="produtos && produtos.length === 0" key="sem-resultados">
        <p class="sem-resultados">Busca sem resultados. Tente buscar outro termo.</p>
      </div>
      <PaginaCarregando v-else key="carregando" />
    </transition>
  </section>
</template>

<script>
import ProdutosPaginar from "@/components/ProdutosPaginar.vue";
import { api } from "@/services.js";
import { serialize } from "@/helpers.js";

export default {
  name: "ProdutosLista",
  components: {
    ProdutosPaginar
  },
  data() {
    return {
      produtos: null,
      produtosPorPagina: 9,
      produtosTotal: 0
    };
  },
  computed: {
    url() {
      const query = serialize(this.$route.query);

      return `/produto?_limit=${this.produtosPorPagina}${query}`;
    }
  },
  methods: {
    getProdutos() {
      this.produtos = null;
      api.get(this.url).then(response => {
        this.produtosTotal = Number(response.headers["x-total-count"]);
        this.produtos = response.data;
      });
    }
  },
  watch: {
    url() {
      this.getProdutos();
    }
  },
  created() {
    this.getProdutos();
  }
};
</script>

<style lang="scss" scoped>
.produtos-container {
  max-width: 1000px;
  margin: 0 auto;
}

.produtos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  margin: 30px;
}

.produto {
  @include shadow_default;
  padding: 10px;
  background: #fff;
  border-radius: 4px;
  @include hover_item;

  img {
    border-radius: 4px;
    margin-bottom: 20px;
  }
}

.titulo {
  @include font;
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.preco {
  color: $third_color;
  font-weight: bold;
}

.sem-resultados {
  text-align: center;
}
</style>