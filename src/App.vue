<template>
  <div id="app">
    <TheHeader />
    <main>
      <transition mode="out-in">
        <router-view />
      </transition>
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

.v-enter,
.v-leave-to {
  opacity: 0;
}

.v-enter {
  transform: translate3d(0, -20px, 0);
}

.v-leave-to {
  transform: translate3d(0, 20px, 0);
}

.v-enter-active,
.v-leave-active {
  transition: all 0.3s;
}
</style>
