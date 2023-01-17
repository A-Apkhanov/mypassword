<template>
  <form :class="$style.password_form" @submit.prevent="generatePassword">
    <div :class="$style.password_wrapper">
      <password-input v-model="password" />
      <password-copy-button
        :disabled="isCopyDisabled"
        :done="isCopyDone"
        @click="copyPassword"
        :class="$style.password_button"
      />
    </div>
    <password-validator :password="password" />
    <app-range id="length" name="length" label="Length" v-model="length" />
    <div :class="$style.password_params">
      <app-checkbox
        name="letters"
        v-model="params.letters"
        id="letters"
        label="Letters"
      />
      <app-checkbox
        name="difCase"
        v-model="params.difCase"
        id="difCase"
        label="Different case"
      />
      <app-checkbox
        name="marks"
        v-model="params.marks"
        id="marks"
        label="Punctuation marks"
      />
      <app-checkbox
        name="numbers"
        v-model="params.numbers"
        id="numbers"
        label="Numbers"
      />
    </div>
    <div class="flex flex-col gap-1">
      <app-button type="submit" :disabled="disabledSubmit">
        Generate
      </app-button>
    </div>
  </form>
</template>

<script>
import PasswordCopyButton from "./PasswordCopyButton.vue";
import PasswordInput from "./PasswordInput.vue";
import PasswordValidator from "./PasswordValidator.vue";
import AppRange from "./AppRange.vue";
import AppCheckbox from "./AppCheckbox.vue";
import AppButton from "./AppButton.vue";

export default {
  name: "PasswordForm",
  components: {
    PasswordCopyButton,
    PasswordInput,
    PasswordValidator,
    AppRange,
    AppCheckbox,
    AppButton,
  },
  data() {
    return {
      password: "",
      length: 12,
      isCopyDisabled: true,
      isCopyDone: false,
      params: {
        letters: true,
        difCase: true,
        marks: true,
        numbers: true,
      },
    };
  },
  methods: {
    generatePassword() {
      const numbers = this.params.numbers ? "0123456789" : "";
      const letters = this.params.letters ? "abcdefghijklmnopqrstuvwxyz" : "";
      const upperLetters = this.params.difCase ? letters.toUpperCase() : "";
      const marks = this.params.marks ? "!@#$%^&*()" : "";
      const chars = numbers + letters + upperLetters + marks;

      let password = "";

      for (let i = 0; i < this.length; i++) {
        const randomNumber = Math.floor(Math.random() * chars.length);
        password += chars.substring(randomNumber, randomNumber + 1);
      }

      this.password = password;
    },
    copyPassword() {
      navigator.clipboard.writeText(this.password).then(() => {
        this.isCopyDone = true;
        setTimeout(() => (this.isCopyDone = false), 500);
      });
    },
  },
  computed: {
    disabledSubmit() {
      return !Object.values(this.params).filter((value) => value === true)
        .length;
    },
  },
  watch: {
    password(newPassword) {
      this.isCopyDisabled = newPassword === "";
    },
  },
};
</script>

<style lang="scss" module>
.password_form {
  width: 100%;
  max-width: 320px;

  display: flex;
  flex-direction: column;
  gap: 12px;

  padding: 20px;
  margin: 10px;

  border-radius: 16px;

  background-color: #f1f8f7;
}

.password_params {
  display: flex;
  flex-direction: column;
}

.password_wrapper {
  position: relative;
}

.password_button {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
