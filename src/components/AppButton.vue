<template>
  <button :type="type" :class="$style.button" :disabled="disabled">
    <slot />
  </button>
</template>

<script>
export default {
  name: "AppButton",
  props: {
    type: {
      type: String,
      default: "button",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" module>
button.button {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  padding: 10px;

  border-radius: 9999px;

  color: white;

  background-color: #2a9d8f;

  outline: none;

  border: 2px solid transparent;

  &:disabled {
    filter: opacity(50%);
  }

  &:hover:not(:active):not(:disabled) {
    filter: brightness(90%);
  }

  &:active:not(:disabled) {
    filter: brightness(110%);
  }

  &:focus-visible:not(:disabled) {
    border-color: #264653;
  }
}
</style>
