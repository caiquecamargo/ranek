<template>
  <section class="usuario">
    <nav class="sidenav">
      <ul>
        <li>
          <router-link :to="{ name: 'usuario' }">Produtos</router-link>
        </li>
        <li>
          <router-link :to="{ name: 'usuarioCompras' }">Compras</router-link>
        </li>
        <li>
          <router-link :to="{ name: 'usuarioVendas' }">Vendas</router-link>
        </li>
        <li>
          <router-link :to="{ name: 'usuarioEditar' }">Esitar Usuário</router-link>
        </li>
        <li>
          <button @click="deslogar">Deslogar</button>
        </li>
      </ul>
    </nav>
    <transition mode="out-in">
      <router-view />
    </transition>
  </section>
</template>

<script>
export default {
  name: "Usuario",
  methods: {
    deslogar() {
      this.$store.dispatch("deslogarUsuario");
      this.$router.push({ name: "login" });
    }
  }
};
</script>

<style lang="scss" scoped>
.usuario {
  display: grid;
  grid-template-columns: minmax(140px, 200px) 1fr;
  max-width: 900px;
  margin: 40px auto;
  gap: 30px;
  padding: 20px;
}

@media screen and (max-width: 500px) {
  .usuario {
    grid-template-columns: 1fr;
    margin: 0 auto;
  }
}

.sidenav {
  a,
  button {
    padding: 10px;
    display: block;
    background: $button_background;
    margin-bottom: 10px;
    border-radius: 4px;
    @include hover_button;

    &.router-link-exact-active {
      background: $second_color;
      color: #fff;
    }
  }

  button {
    border: none;
    width: 100%;
    font-size: 1rem;
    text-align: left;
    cursor: pointer;
  }
}
</style>