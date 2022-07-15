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
        :data-myiter="iter"
      >
        <Hexagon :size="90" :border-size="0" :backgroundColor="item" v-ripple />
      </div>
    </div>
  </div>
</template>

<script>
import Hexagon from "@coddicat/vue-hexagon";
import convert from "color-convert";

const pi = 3.14159;

export default {
  props: ["id", "color", "iter"],
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
    gneRndNum(lower, upper) {
      const range = upper - lower;
      return lower + Math.random() * range;
    },
    reverseOverflow(lower, upper, value) {
      if (value < lower) {
        return lower + (lower - value);
      } else if (value > upper) {
        return upper - (value - upper);
      } else {
        return value;
      }
    },
    genRndHex(color, inIter) {
      var [h, s, v] = convert.hex.hsl(color);

      var hexAry = [];
      hexAry.push("#" + convert.hsl.hex(h, s, v).toLowerCase());
      for (let i = 0; i < 6; i++) {
        var new_h = h + this.gneRndNum(-10, 10);
        var new_s = s + this.gneRndNum(-20, 20);
        var new_v = v + this.gneRndNum(-20, 20);

        new_h = this.reverseOverflow(0, 359, new_h)
        new_s = this.reverseOverflow(0, 100, new_s)
        new_v = this.reverseOverflow(0, 100, new_v)

        hexAry.push("#" + convert.hsl.hex(new_h, new_s, new_v).toLowerCase());
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
      return this.genRndHex(this.color, this.iter);
    },
  },
  created() {
    this.genHexPos();
  },
};
</script>

<style>
.hex-container {
  height: 300px;
  width: 300px;

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
.hex-comp,
.hex-comp div {
  border-radius: 90px;
}
</style>