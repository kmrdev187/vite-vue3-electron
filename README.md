# Vue 3 + Vite + Electron

The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Ipc usage

### In render process

```vue
<script setup>
import { ref } from "vue";

const response = ref("");

function sendToMain(message) {
  window.ipc.send("toMain", message);
  window.ipc.receive("fromMain", (r) => {
    response.value = r;
  });
}
</script>

<template>
  <button type="button" @click="sendToMain('Hello')">Send</button>
  <span>{{ response }}</span>
</template>
```

### In main process

```js
const { ipcMain } = require("electron");

const mainWindow = new BrowserWindow({
  //...
});

//...

ipcMain.on("toMain", (event, arg) => {
  mainWindow.webContents.send("fromMain", `Your message is: ${arg}`);
});
```

## Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)
