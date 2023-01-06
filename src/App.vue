<template>
  <div id="app" class="flex flex-col min-h-screen">
    <header class="bg-sky-700">
      <div class="max-w-7xl mx-auto p-4">
        <span class="text-sky-50 text-xl">MyPassword</span>
      </div>
    </header>
    <main class="flex-auto flex justify-center items-center bg-sky-700">
      <form
        class="flex flex-col gap-3 w-full max-w-xs m-2.5 p-2.5 rounded bg-blue-50"
        @submit.prevent="generatePassword"
      >
        <label for="password">Password</label>
        <input
          type="text"
          placeholder="Password"
          id="password"
          class="p-2"
          v-model="password"
        />
        <label for="length">Length (4-64): {{ length }}</label>
        <input
          type="range"
          id="length"
          name="vol"
          min="4"
          max="64"
          v-model="length"
        />
        <div class="flex flex-col">
          <div class="flex gap-2">
            <input
              type="checkbox"
              id="letters"
              name="letters"
              v-model="letters"
            />
            <label for="letters">Letters</label>
          </div>
          <div class="flex gap-2">
            <input type="checkbox" id="case" name="case" v-model="difCase" />
            <label for="case">Different case</label>
          </div>
          <div class="flex gap-2">
            <input type="checkbox" id="marks" name="marks" v-model="marks" />
            <label for="marks">Punctuation marks</label>
          </div>
          <div class="flex gap-2">
            <input
              type="checkbox"
              id="numbers"
              name="numbers"
              v-model="numbers"
            />
            <label for="numbers">Numbers</label>
          </div>
        </div>
        <div class="flex gap-1">
          <button
            type="submit"
            class="flex-auto p-1 bg-blue-500 rounded-sm text-sky-50 hover:bg-sky-600 active:bg-blue-400"
          >
            Generate
          </button>
          <button
            type="button"
            class="flex-auto p-1 bg-blue-500 rounded-sm text-sky-50 hover:bg-sky-600 active:bg-blue-400"
            @click="copyPassword"
          >
            Copy
          </button>
        </div>
      </form>
    </main>
    <footer class="text-center bg-sky-700">
      <span class="text-sky-50 text-xs">© 2023 Apkahnov Aleksand</span>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      password: "",
      length: 12,
      letters: true,
      difCase: true,
      marks: true,
      numbers: true,
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
      navigator.clipboard.writeText(this.password);
    },
  },
};
</script>
