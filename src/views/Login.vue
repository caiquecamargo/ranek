<template>
  <section class="login">
    <h1 class="titulo">Login</h1>
    <form>
      <label for="email">Email</label>
      <input type="email" name="email" id="email" v-model="login.email" />
      <label for="senha">Senha</label>
      <input type="password" name="senha" id="senha" v-model="login.senha" />
      <button class="btn" @click.prevent="logar">Logar</button>
    </form>
    <p class="perdeu">
      <a href="/" target="_black">Recuperar senha</a>
    </p>
    <LoginCriar />
  </section>
</template>

<script>
import LoginCriar from "@/components/LoginCriar.vue";

export default {
  name: "Login",
  components: {
    LoginCriar
  },
  data() {
    return {
      login: {
        email: "",
        senha: ""
      }
    };
  },
  methods: {
    logar() {
      this.$store.dispatch("getUsuario", this.login.email);
      this.$router.push({ name: "usuario" });
    }
  }
};
</script>

<style lang="scss" scoped>
.login {
  max-width: 500px;
  margin: 0 auto;
  padding: 0 20px;
}

.titulo {
  text-align: center;
  margin-top: 40px;
  color: $second_color;
  font-size: 1.8rem;
  font-weight: bold;
}

form {
  display: grid;
}

.btn {
  @include button;
  width: 100%;
  max-width: 300px;
  margin-left: auto;
  margin-right: auto;
}

.perdeu {
  text-align: center;
  margin: 20px auto 0 auto;

  a {
    @include link_hover;
  }
}
</style>