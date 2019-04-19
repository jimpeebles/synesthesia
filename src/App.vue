<template>
  <div class="container" :style="{'--r': this.r,'--g': this.g,'--b': this.b}">
    <input @input="colorMash($event)" class="thebox" type="text">
  </div>
</template>

<script>
export default {
  data() {
    return {
      r: 50,
      g: 146,
      b: 100,
      timeSinceLastKey: 0
    };
  },
  methods: {
    colorMash($event) {}
  }
};
</script>

<style id="styles">
html,
body {
  margin: 0;
  padding: 0;
}
.container {
  --r: 200;
  --g: 152;
  --b: 18;

  display: flex;
  align-items: center;
  justify-content: center;

  margin: 0;
  padding: 0;
  height: 100vh;
  overflow: hidden;

  background-color: rgba(var(--r), var(--g), var(--b), 0.5);
}
.thebox {
  background-color: rgba(0, 0, 0, 0);
  font-size: 10vw;
  outline: none;
  box-shadow: none;
  border: none;
  text-align: center;
  caret-color: #fff;
}
</style>
