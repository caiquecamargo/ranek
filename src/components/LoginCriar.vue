<template>
  <section class="criar-conta">
    <h2 class="titulo">Crie sua conta</h2>
    <transition-group mode="out-in">
      <button v-if="!criar" @click="criar =true" class="button" key="button">Criar conta</button>
      <UsuarioForm v-else key="form">
        <button class="button" @click.prevent="criarUsuario">Criar usuário</button>
      </UsuarioForm>
    </transition-group>
  </section>
</template>

<script>
import UsuarioForm from "@/components/UsuarioForm.vue";

export default {
  name: "LoginCriar",
  components: {
    UsuarioForm
  },
  data() {
    return {
      criar: false
    };
  },
  methods: {
    async criarUsuario() {
      try {
        await this.$store.dispatch("criarUsuario", this.$store.state.usuario);
        await this.$store.dispatch(
          "getUsuario",
          this.$store.state.usuario.email
        );
        this.$router.push({ name: "usuario" });
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.titulo {
  margin-top: 40px;
  margin-bottom: 10px;
  text-align: center;
  font-size: 1.5rem;
  font-weight: bold;
}

.button {
  @include button;
  width: 100%;
  max-width: 300px;
  margin: 0 auto;
}
</style>