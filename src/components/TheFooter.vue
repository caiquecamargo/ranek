<template>
  <footer>
    <p>Ranek. Alguns direitos reservados.</p>
  </footer>
</template>

<script>
export default {
  name: "TheFooter"
};
</script>

<style lang="scss" scoped>
footer {
  background: $second_color;
  padding: 25px 0;
  @include font;
  text-align: center;
  font-size: 1.2rem;
  color: white;
  position: relative;
  top: 75px;
}
</style>