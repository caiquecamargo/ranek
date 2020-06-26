<template>
  <form class="adicionar-produto">
    <label for="nome">Nome</label>
    <input type="text" name="nome" id="nome" v-model="produto.nome" />
    <label for="preco">Preço (R$)</label>
    <input type="number" name="preco" id="preco" v-model="produto.preco" />
    <label for="fotos">Fotos</label>
    <input type="file" name="fotos" id="fotos" multiple ref="fotos" />
    <label for="descricao">Descrição</label>
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
      const form = new FormData();

      const files = this.$refs.fotos.files;

      if (files) {
        for (let i = 0; i < files.lenght; i++) {
          form.append(files[i].name, files[i]);
        }
      }

      form.append("nome", this.produto.nome);
      form.append("preco", this.produto.preco);
      form.append("descricao", this.produto.descricao);
      form.append("vendido", this.produto.vendido);
      form.append("usuario_id", this.$store.state.usuario.id);

      return form;
    },
    adicionarProduto() {
      const produto = this.formatarProduto();
      api.post("/produto", produto).then(response => {
        console.log(response);
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