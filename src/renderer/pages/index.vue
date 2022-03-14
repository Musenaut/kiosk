<template>
  <div class="e-nuxt-container">
    <div class="">
      <h1>mKiosk</h1>
      <p>Version{{ version }}</p>
    </div>
  </div>
</template>

<script>

const { ipcRenderer } = require('electron');
export default {
  name: 'IndexPage',
  data () {
    return {
      version: null,
    }
  },
  mounted(){
    this.getVersion();
  },
  methods: {
    getVersion(){
      ipcRenderer.send('app_version');
      ipcRenderer.on('app_version', (event, arg) => {
        ipcRenderer.removeAllListeners('app_version');
        this.version = 'Version ' + arg.version;
      });
    }

  }
}
</script>
