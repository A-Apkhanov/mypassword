<template>
  <div :class="$style.wrapper">
    <label :for="id">{{ label }}: {{ value }}</label>
    <input
      type="range"
      :id="id"
      :name="name"
      :min="min"
      :max="max"
      :value="value"
      @input="$emit('input', $event.target.value)"
      :class="$style.input"
      :style="{
        'background-size': `${((value - min) / (max - min)) * 100}% 100%`,
      }"
    />
  </div>
</template>

<script>
export default {
  name: "AppRange",
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    min: {
      type: Number,
      default: 8,
    },
    max: {
      type: Number,
      default: 64,
    },
    value: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style lang="scss" module>
.wrapper {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.input {
  -webkit-appearance: none;
  width: 100%;
  height: 5px;
  background: #e2e8f0;
  border-radius: 2px;
  background-image: linear-gradient(#2a9d8f, #2a9d8f);
  background-repeat: no-repeat;
}

.input::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 18px;
  width: 18px;
  border-radius: 50%;
  background: #2a9d8f;
  cursor: ew-resize;
  box-shadow: 0 0 1px 0 #555;
  transition: background 0.3s ease-in-out;
}

.input::-webkit-slider-runnable-track {
  -webkit-appearance: none;
  box-shadow: none;
  border: none;
  background: transparent;
}
</style>
