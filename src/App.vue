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
        <label
          for="password"
          class="absolute overflow-hidden w-px h-px p-0 border-0"
        >
          Password
        </label>
        <div class="flex relative">
          <input
            type="text"
            placeholder="Password"
            id="password"
            class="flex-auto p-3 pr-12 rounded-lg bg-slate-200 focus:bg-blue-600/10"
            v-model="password"
          />
          <button
            type="button"
            class="group absolute inset-y-0 right-0 rounded-lg p-3 bg-transparent focus:outline-none focus:shadow-outline"
            @click="copyPassword"
            :disabled="isCopyDisabled"
          >
            <icon-done v-if="isCopyDone" />
            <icon-copy v-else />
          </button>
        </div>
        <password-validator :password="password" />
        <div class="flex flex-col gap-2">
          <label for="length">Length: {{ length }}</label>
          <input
            type="range"
            id="length"
            name="vol"
            min="8"
            max="64"
            v-model="length"
          />
        </div>
        <div class="flex flex-col">
          <div class="flex gap-2 items-center">
            <input
              type="checkbox"
              id="letters"
              name="letters"
              v-model="letters"
              class="w-4 h-4"
            />
            <label for="letters">Letters</label>
          </div>
          <div class="flex gap-2 items-center">
            <input
              type="checkbox"
              id="case"
              name="case"
              v-model="difCase"
              class="w-4 h-4"
            />
            <label for="case">Different case</label>
          </div>
          <div class="flex gap-2 items-center">
            <input
              type="checkbox"
              id="marks"
              name="marks"
              v-model="marks"
              class="w-4 h-4"
            />
            <label for="marks">Punctuation marks</label>
          </div>
          <div class="flex gap-2 items-center">
            <input
              type="checkbox"
              id="numbers"
              name="numbers"
              v-model="numbers"
              class="w-4 h-4"
            />
            <label for="numbers">Numbers</label>
          </div>
        </div>
        <div class="flex flex-col gap-1">
          <app-button
            type="submit"
            :disabled="!letters && !marks && !difCase && !numbers"
          >
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
import IconCopy from "./components/icons/IconCopy.vue";
import IconDone from "./components/icons/IconDone.vue";
import PasswordValidator from "./components/PasswordValidator.vue";
import AppButton from "./components/AppButton.vue";

export default {
  name: "App",
  components: { AppButton, PasswordValidator, IconDone, IconCopy },
  data() {
    return {
      password: "",
      length: 12,
      letters: true,
      difCase: true,
      marks: true,
      numbers: true,
      isCopyDone: false,
      isCopyDisabled: true,
    };
  },
  methods: {
    generatePassword() {
      const numbers = this.numbers ? "0123456789" : "";
      const letters = this.letters ? "abcdefghijklmnopqrstuvwxyz" : "";
      const upperLetters = this.difCase ? letters.toUpperCase() : "";
      const marks = this.marks ? "!@#$%^&*()" : "";
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
  watch: {
    password(newPassword) {
      this.isCopyDisabled = newPassword === "";
    },
  },
};
</script>
