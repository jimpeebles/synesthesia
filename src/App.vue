<template>
  <div class="container" :style="{'--r': this.r,'--g': this.g,'--b': this.b, '--a':this.a}">
    <input @input="colorMash($event)" v-model="txtin" class="thebox" type="text">
  </div>
</template>

<script>
export default {
  data() {
    return {
      r: 50,
      g: 146,
      b: 100,
      txtin: "",
      currentTimeSinceLastKey: 0,
      minTSL: 0,
      maxTSL: 0,
      a: 0,
      buffer: [100, 100, 100]
    };
  },
  methods: {
    colorMash(event) {
      let keycode = this.txtin.charCodeAt(0);
      this.txtin = event.target.value.charAt(0);
      let normalized = this.normalize(keycode, 0, 177);
      let rgbval = normalized * 255;
      this.buffer.push(rgbval);
      // this.buffer[0] = this.buffer[1];
      // this.buffer[1] = this.buffer[2];
      // this.buffer[2] = normalized * 255;
      console.log(this.buffer.shift());
      this.r = this.buffer[0];
      this.g = this.buffer[1];
      this.b = this.buffer[2];
    },
    normalize(val, min, max) {
      return (val - min) / (max - min);
    }
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
  --a: 0;

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
