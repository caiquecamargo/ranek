<template>
  <form>
    <div class="usuario" v-if="mostrarDadosLogin">
      <label for="nome">Nome</label>
      <input type="text" name="nome" id="nome" v-model="nome" />
      <label for="email">Email</label>
      <input type="email" name="email" id="email" v-model="email" />
      <label for="senha">Senha</label>
      <input type="password" name="senha" id="senha" v-model="senha" />
    </div>
    <label for="cep">Cep</label>
    <input type="text" name="cep" id="cep" v-model="cep" />
    <label for="endereco">Endereco</label>
    <input type="text" name="endereco" id="endereco" v-model="endereco" />
    <label for="bairro">Bairro</label>
    <input type="text" name="bairro" id="bairro" v-model="bairro" />
    <label for="cidade">Cidade</label>
    <input type="text" name="cidade" id="cidade" v-model="cidade" />
    <label for="estado">Estado</label>
    <input type="text" name="estado" id="estado" v-model="estado" />
    <div class="button">
      <slot />
    </div>
  </form>
</template>

<script>
import { mapFields } from "@/helpers.js";
import { getCep } from "@/services.js";

export default {
  name: "UsuarioForm",
  method: {
    preencherCep() {
      const cep = this.cep.replace(/\D/g, "");
      if (cep.length === 8) {
        getCep(cep).then(response => {
          this.endereco = response.data.logradouro;
          this.bairro = response.data.bairro;
          this.cidade = response.data.localidade;
          this.estado = response.data.uf;
        });
      }
    }
  },
  computed: {
    ...mapFields({
      fields: [
        "nome",
        "email",
        "senha",
        "cep",
        "endereco",
        "bairro",
        "cidade",
        "estado"
      ],
      base: "usuario",
      mutation: "UPDATE_USUARIO"
    }),
    mostrarDadosLogin() {
      return !this.$store.state.login || this.$route.name === "usuarioEditar";
    }
  }
};
</script>

<style lang="scss" scoped>
form,
.usuario {
  display: grid;
  grid-template-columns: 80px 1fr;
  align-items: center;
}

.usuario {
  grid-column: 1 / 3;
}

.button {
  grid-column: 1 / -1;
  margin-top: 10px;
}
</style>