<template>
  <div :class="$style.root">
    <div :class="[$style.password_validity, modifierClass]">
      <span v-for="i in 3" :key="i" :class="$style.pill" />
    </div>
  </div>
</template>

<script>
export default {
  name: "PasswordValidator",
  props: {
    password: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      passwordStrength: 0,
    };
  },
  methods: {
    evaluatePasswordStrength(password) {
      let strength = 0;
      if (password.length >= 8) {
        strength += 1;
      }
      if (/[A-Z]/.test(password)) {
        strength += 1;
      }
      if (/[a-z]/.test(password)) {
        strength += 1;
      }
      if (/[0-9]/.test(password)) {
        strength += 1;
      }
      if (/[!@#$%^&*()]/.test(password)) {
        strength += 1;
      }
      return strength;
    },
  },
  computed: {
    modifierClass() {
      if (!this.password) return null;
      if (this.passwordStrength <= 2) {
        return [this.$style.password_validity__weak];
      }
      if (this.passwordStrength <= 4) {
        return [this.$style.password_validity__good];
      }
      return [this.$style.password_validity__strong];
    },
  },
  watch: {
    password(newPassword) {
      this.passwordStrength = this.evaluatePasswordStrength(newPassword);
    },
  },
};
</script>

<style lang="scss" module>
.root {
  display: flex;
  flex-direction: column;
}

.password_validity {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 10px;

  &__weak .pill:first-of-type {
    background-color: #e76f51;
  }

  &__good .pill:not(:last-of-type) {
    background-color: #e9c46a;
  }

  &__strong .pill {
    background-color: #2a9d8f;
  }
}

.pill {
  display: block;
  height: 5px;
  background-color: #eef3f2;
  border-radius: 2px;
}
</style>
