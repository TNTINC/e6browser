<template>
  <div id="app">
    <E621Search />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import E621Search from './components/E621Search.vue';

@Component({
  components: {
    E621Search,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html {
  background: #1b1d20;
  width: 100vw;
}

body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
