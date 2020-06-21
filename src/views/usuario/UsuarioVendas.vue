<template>
  <section class="vendas">
    <div v-if="vendas">
      <h2>Vendas</h2>
      <div class="produtos-wrapper" v-for="(venda, index) in vendas" :key="index">
        <ProdutoItem v-if="venda" :produto="venda.produto">
          <p class="comprador">
            <span>Comprador:</span>
            {{compra.comprador_id}}
          </p>
        </ProdutoItem>
        <div class="entrega">
          <h3>Entrega:</h3>
          <ul v-if="venda.endereco">
            <li v-for="(value, key) in venda.endereco" :key="key">{{key}}: {{value}}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ProdutoItem from "@/components/ProdutoItem.vue";
import { api } from "@/services.js";
import { mapState } from "vuex";

export default {
  name: "UsuarioVendas",
  components: {
    ProdutoItem
  },
  data() {
    return {
      vendas: null
    };
  },
  computed: {
    ...mapState(["usuario", "login"])
  },
  methods: {
    getVendas() {
      api
        .get(`/transacao?vendedor_id=${this.usuario.id}`)
        .then(response => (this.vendas = response.data));
    }
  },
  watch: {
    login() {
      this.getVendas();
    }
  },
  created() {
    if (this.login) {
      this.getVendas();
    }
  }
};
</script>

<style lang="scss" scoped>
.produto-wrapper {
  margin-bottom: 40px;
}

.comprador {
  span {
    color: $third_color;
  }
}

h2 {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 20px;
}

.entrega {
  display: grid;
  grid-template-columns: minmax(100px, 200px) 1fr;
}

h3 {
  justify-self: end;
}
</style>