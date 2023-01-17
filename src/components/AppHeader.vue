<template>
  <header :class="$style.header">
    <span :class="$style.logo">MyPassword</span>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
};
</script>

<style lang="scss" module>
.header {
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  padding: 16px;
}

.logo {
  color: #fff;
  font-size: 20px;
}
</style>
