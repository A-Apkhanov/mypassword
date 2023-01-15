<template>
  <div>
    <input
      type="checkbox"
      :name="name"
      :checked="value"
      @change="$emit('input', $event.target.checked)"
      :class="$style.checkbox"
      :id="id"
    />
    <label :for="id" :class="$style.label">{{ label }}</label>
  </div>
</template>

<script>
export default {
  name: "AppCheckbox",
  props: {
    id: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    value: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style lang="scss" module>
.checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
  width: 0;
  height: 0;
}

.label {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.checkbox + .label::before {
  content: "";
  display: inline-block;
  width: 16px;
  height: 16px;
  flex-shrink: 0;
  flex-grow: 0;
  border: 1px solid #adb5bd;
  border-radius: 2px;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
  background-color: #eef3f2;
}

.checkbox:checked + .label::before {
  border-color: #2a9d8f;
  background-color: #2a9d8f;
  background-position: 50% 50%;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
}

.checkbox:not(:disabled):checked + .label:hover:before {
  filter: brightness(90%);
}

.checkbox:not(:disabled):checked + .label:active:before {
  filter: brightness(110%);
}

.checkbox:not(:disabled):not(:checked) + .label:hover:before {
  border-color: #2a9d8f;
  filter: brightness(90%);
}

.checkbox:not(:disabled):not(:checked) + .label:active:before {
  border-color: #2a9d8f;
  filter: brightness(110%);
}

.checkbox:disabled + .label::before {
  filter: opacity(50%);
}
</style>
