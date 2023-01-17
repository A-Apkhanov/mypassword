<template>
  <div id="app" :class="$style.root">
    <app-header />
    <main :class="$style.main">
      <password-form />
    </main>
    <app-footer />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import PasswordForm from "./components/PasswordForm.vue";

export default {
  name: "App",
  components: {
    PasswordForm,
    AppFooter,
    AppHeader,
  },
};
</script>

<style lang="scss" module>
.root {
  display: flex;
  flex-direction: column;
  height: auto;
  min-height: 100vh;
  background-image: url("~/assets/background.svg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  background-attachment: fixed;
}

.main {
  flex: 1 1 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
