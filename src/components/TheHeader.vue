<template>
  <header>
    <nav>
      <router-link to="/" class="logo">
        <img src="@/assets/ranek.svg" alt="Ranek" />
      </router-link>
      <router-link v-if="$store.state.login" to="/usuario" class="btn">{{nome}}</router-link>
      <router-link v-else to="/login" class="btn">Vender / Login</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: "TheHeader",
  computed: {
    nome() {
      return this.$store.state.usuario.nome;
    }
  }
};
</script>

<style lang="scss" scoped>
.btn {
  @include button;
}

nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px 20px;
  @include shadow_default;
}

.logo {
  padding: 10px 0;

  img {
    width: 90px;
  }
}
</style>