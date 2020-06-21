<template>
  <form class="adicionar-produto">
    <label for="nome">Nome</label>
    <input type="text" name="nome" id="nome" v-model="produto.nome" />
    <label for="preco">Preço (R$)</label>
    <input type="number" name="preco" id="preco" v-model="produto.preco" />
    <label for="fotos">Fotos</label>
    <input type="file" name="fotos" id="fotos" ref="fotos" />
    <label for="descricao">Preço (R$)</label>
    <input type="textarea" name="descricao" id="descricao" v-model="produto.descricao" />
    <input class="btn" type="button" value="Adicionar Produto" @click.prevent="adicionarProduto" />
  </form>
</template>

<script>
import { api } from "@/services.js";

export default {
  name: "ProdutosAdicionar",
  data() {
    return {
      produto: {
        nome: "",
        preco: "",
        descricao: "",
        fotos: null,
        vendido: "false"
      }
    };
  },
  methods: {
    formatarProduto() {
      this.produto.usuario_id = this.$store.state.usuario.id;
    },
    adicionarProduto() {
      this.formatarProduto();
      api.post("/produto", this.produto).then(() => {
        this.$store.dispatch("getUsuarioProdutos");
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.adicionar-produto {
  display: grid;
  grid-template-columns: 100px 1fr;
  align-items: center;
  margin-bottom: 60px;
}

.btn {
  @include button;
  grid-column: 1 / -1;
}
</style>