<template>
  <transition>
    <ul class="erro" v-if="erro.lenght > 0">
      <li v-for="(erro, index) in erros" :key="index" v-html="erro"></li>
    </ul>
  </transition>
</template>

<script>
export default {
  name: "ErroNotificacao",
  props: {
    erros: []
  }
};
</script>

<style lang="scss" scoped>
.erro {
  margin: 20px auto;

  li {
    color: $third_color;
    text-align: center;
  }
}
</style>