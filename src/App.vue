<template>
  <div class="container" :style="{'--r': this.r,'--g': this.g,'--b': this.b, '--a':this.a}">
    <input @keyup="colorMash($event)" :value="txtin" class="thebox" type="text" autofocus>
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
      // Clear input box
      this.txtin = "";

      // Get keycode for input event
      let keycode = event.keyCode;

      // Normalize keycode (range: 0-177) to RGB value (0-255)
      let normalized = this.normalize(keycode, 0, 177);
      let rgbval = normalized * 255;

      // Add value to buffer and remove first item to keep only last 3 values
      this.buffer.push(rgbval);
      this.buffer.shift();

      // Set RGB values based on buffer contents
      this.r = this.buffer[0];
      this.g = this.buffer[1];
      this.b = this.buffer[2];
    },

    // Function to normalize value within a given range
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
  font-family: Poppins, Arial, Helvetica, sans-serif;
  font-size: 80vh;
  font-weight: 700;
  color: #fff;
  outline: none;
  box-shadow: none;
  border: none;
  text-align: center;
  caret-color: #fff;
}
</style>
