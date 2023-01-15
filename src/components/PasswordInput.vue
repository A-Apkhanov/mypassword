<template>
  <div>
    <label for="password" :class="$style.visually_hidden"> Password </label>
    <input
      type="text"
      placeholder="Password"
      id="password"
      :class="$style.input"
      :value="value"
      @input="$emit('input', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: "PasswordInput",
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isCopyDone: false,
      isCopyDisabled: true,
    };
  },
};
</script>

<style lang="scss" module>
.wrapper {
  display: flex;
  position: relative;
}

.input {
  width: 100%;
  padding: 12px 48px 12px 12px;
  background-color: #eef3f2;
  border-radius: 8px;
  border: 2px solid transparent;
  outline: none;
}

.input:focus-visible {
  border-color: #2a9d8f;
}

.visually_hidden {
  position: absolute;

  overflow: hidden;
  clip: rect(0 0 0 0);

  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;

  white-space: nowrap;

  border: 0;

  clip-path: inset(100%);
}
</style>
