<template>
  <div class="hex-container">
    <div class="hex-origin">
      <div
        class="hex-comp"
        v-for="(item, index) in hexAry"
        :key="index"
        :style="{
          transform: `translate(-50%, -50%) translateX(${posAry[index].x}px) translateY(${posAry[index].y}px)`,
        }"
        @click="sendOut(item, id)"
      >
        <Hexagon :size="90" :border-size="0" :backgroundColor="item" />
      </div>
    </div>
  </div>
</template>

<script>
import Hexagon from "@coddicat/vue-hexagon";
import hexToHsl from "hex-to-hsl";
import hslToHex from "hsl-to-hex";

const pi = 3.14159;

export default {
  props: ["id", "color"],
  components: { Hexagon },
  data() {
    return {
      posAry: [],
    };
  },
  methods: {
    sendOut(outcolor, outid) {
      this.$emit("result", outcolor, outid);
    },
    gneRndNum(lower, upper){
      const range = upper - lower;
      return lower + Math.random() * range
    },
    genRndHex(color) {
      var [h, s, v] = hexToHsl(color);
      var hexAry = [];
      hexAry.push(hslToHex(h, s, v));
      for (let i = 0; i < 6; i++) {
        const new_h = h + this.gneRndNum(-10,10);
        const new_s = s + this.gneRndNum(-20,20);
        const new_v = v + this.gneRndNum(-20,20);

        hexAry.push(hslToHex(new_h, new_s, new_v));
      }
      return hexAry;
    },
    degToRad(deg) {
      return (deg * pi) / 180;
    },
    pushToPosAry(x, y) {
      const pos = { x, y };
      this.posAry.push(pos);
    },
    genHexPos() {
      var radius = 100;
      var stepDeg = 60;
      var deg = 90;
      var x = 0;
      var y = 0;

      // init push
      this.pushToPosAry(x, y);

      // circle arrangement push
      for (let i = 0; i < 6; i++) {
        x = Math.round(radius * Math.cos(this.degToRad(deg)) * 100) / 100;
        y = Math.round(radius * Math.sin(this.degToRad(deg)) * 100) / 100;

        this.pushToPosAry(x, y);

        deg += stepDeg;
      }
    },
  },
  computed: {
    hexAry() {
      return this.genRndHex(this.color);
    },
  },
  created() {
    this.genHexPos();
  },
};
</script>

<style>
.hex-container {
  height: 320px;
  width: 40%;

  position: relative;
}
.hex-origin {
  position: relative;
  left: 50%;
  top: 50%;
}
.hex-comp {
  display: inline-block;
  position: absolute;
}
</style>