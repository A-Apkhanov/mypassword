<template>
  <div
    id="app"
    class="flex flex-col min-h-screen bg-gradient-to-r from-cyan-500 to-blue-500"
  >
    <header>
      <div class="max-w-7xl mx-auto p-4 flex justify-center">
        <span class="text-sky-50 text-xl">MyPassword</span>
      </div>
    </header>
    <main class="flex-auto flex justify-center items-center">
      <form
        class="flex flex-col gap-3 w-full max-w-xs m-2.5 p-5 rounded-2xl bg-slate-50"
        @submit.prevent="generatePassword"
      >
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
        <div class="flex flex-col">
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
    </main>
    <footer class="text-center">
      <span class="text-sky-50 text-xs">© 2023 Apkahnov Aleksandr</span>
    </footer>
  </div>
</template>

<script>
import PasswordInput from "./components/PasswordInput.vue";
import PasswordValidator from "./components/PasswordValidator.vue";
import AppButton from "./components/AppButton.vue";
import AppCheckbox from "./components/AppCheckbox.vue";
import AppRange from "./components/AppRange";
import PasswordCopyButton from "@/components/PasswordCopyButton";

export default {
  name: "App",
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
.password_wrapper {
  position: relative;
}
.password_button {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
