<template>
  <button
    type="button"
    :class="$style.button"
    v-on="$listeners"
    :disabled="disabled"
  >
    <icon-done v-if="done" />
    <icon-copy v-else />
  </button>
</template>

<script>
import IconCopy from "./icons/IconCopy";
import IconDone from "./icons/IconDone";

export default {
  name: "PasswordCopyButton",
  components: { IconCopy, IconDone },
  props: {
    disabled: {
      type: Boolean,
      required: true,
    },
    done: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style lang="scss" module>
.button {
  padding: 12px;
  background-color: transparent;
  border: 2px solid transparent;
  border-radius: 8px;
  outline: none;
}

.button svg {
  stroke: #2a9d8f;
}

.button:disabled svg {
  stroke: #a0a4a4;
}

.button:hover:not(:active):not(:disabled) svg {
  filter: brightness(90%);
}

.button:active:not(:disabled) svg {
  filter: brightness(110%);
}
</style>
