<template>
  <div id="app">
    <h1>
      Cycles
      <br />
      {{ cycles }}
    </h1>
    <h1>Pomodoro Clock</h1>
    <app-main v-on:incrementCycle="cycles++"></app-main>
  </div>
</template>

<script>
import Main from './components/Main.vue'
export default {
  name: "App",
  components: {
    'app-main': Main
  },
  data() {
    return {
      cycles: 0,
    };
  },
};
</script>

<style>
html,
body {
  min-height: 100vh;
  margin: 0;
  padding: 0;
  width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
#app {
  display: flex;
  align-items: center;
  /* justify-content: space-between; */
  flex-direction: column;
  min-height: 100vh;
  text-align: center;
  color: #fff;
  background: linear-gradient(
      to top,
      #00071f,
      #010823,
      #020a26,
      #030b2a,
      #040c2d,
      #101237,
      #1f1440,
      #2f1447,
      #511251,
      #730a54,
      #940050,
      #b10046
    )
    fixed;
}
</style>
