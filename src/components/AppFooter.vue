<template>
  <footer :class="$style.footer">
    <span class="text-sky-50 text-xs">© 2023 Apkahnov Aleksandr</span>
  </footer>
</template>

<script>
export default {
  name: "AppFooter",
};
</script>

<style lang="scss" module>
.footer {
  text-align: center;
}
.copyright {
  color: #fff;
  font-size: 12px;
}
</style>
