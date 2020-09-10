<template>
  <div class="about">
    <h1>This is an about page</h1>

    <v-text-field @change="change"></v-text-field>
    <pre>{{ message }}</pre>
  </div>
</template>

<script lang="ts">
import { IpcRenderer } from 'electron';
import Vue from 'vue';
// import { ipcRenderer } from 'electron';

export default Vue.extend({
  name: 'About',
  data: () => {
    return {
      message: 'hello',
    };
  },
  methods: {
    change(text: string) {
      const { ipcRenderer } = window.require('electron');
      (ipcRenderer as IpcRenderer)
        .invoke('loadfile', text)
        .then((_: any) => (console.log(_), (this.message = _.toString())))
        .catch((e: any) => (console.warn(e), (this.message = e.toString())));
    },
  },
});
</script>
