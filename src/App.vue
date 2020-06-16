<template>
  <div id="app">
    <TheHeader />
    <main>
      <router-view />
    </main>
    <TheFooter />
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader.vue";
import TheFooter from "@/components/TheFooter.vue";

export default {
  components: {
    TheHeader,
    TheFooter
  }
};
</script>

<style lang="scss">
@import "scss/normalize.scss";
@import "scss/reset.scss";
@import "scss/settings.scss";

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;

  main {
    flex: 1;
  }
}
</style>
