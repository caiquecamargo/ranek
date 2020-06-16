<template>
  <header>
    <nav>
      <router-link to="/" class="logo">
        <img src="@/assets/ranek.svg" alt="Ranek" />
      </router-link>
      <router-link to="/login" class="btn">Vender / Login</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: "TheHeader"
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