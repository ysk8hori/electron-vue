<template>
  <div class="about">
    <h1>This is an about page</h1>

    <v-text-field @change="change"></v-text-field>
  </div>
</template>

<script lang="ts">
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
      console.log(text);
      try {
        require('electron')
          .ipcRenderer.invoke('click', this.message)
          .then((_: any) => console.log(_))
          .catch((e: any) => console.warn(e));
      } catch (e) {
        console.warn(e);
      }
    },
  },
});
</script>
