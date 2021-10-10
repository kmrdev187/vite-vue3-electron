<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
});

function messageToMain(message) {
  window.ipc.send("toMain", message);
  window.ipc.receive("fromMain", (message) => {
    mainMessage.value = message;
  });
}

const mainMessage = ref("");

const count = ref(0);
</script>

<template>
  <h1>{{ msg }}</h1>

  <p>
    Recommended IDE setup:
    <a href="https://code.visualstudio.com/" target="_blank">VSCode</a>
    +
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
  </p>

  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank">
      Vite Documentation
    </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Documentation</a>
    |
    <a href="https://www.electronjs.org/docs/latest/" target="_blank"
      >Electron Documentation</a
    >
  </p>

  <button type="button" @click="count++">count is: {{ count }}</button>
  <button type="button" @click="messageToMain('Hello Electron')">
    Send message to Electorn
  </button>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
  <span>{{ mainMessage }}</span>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
