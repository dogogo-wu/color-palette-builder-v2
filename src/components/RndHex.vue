<template>
  <div class="hex-container">
    <div v-for="(item, index) in hexAry" :key="index" style="">
      <Hexagon
        class="hex-comp"
        :size="80"
        :border-size="0"
        :backgroundColor="item"
      />
    </div>
  </div>
</template>

<script>
import Hexagon from "@coddicat/vue-hexagon";
import hexToHsl from "hex-to-hsl";
import hslToHex from "hsl-to-hex";

export default {
  props: ["id", "color"],
  components: { Hexagon },
  data() {
    return {
      //   hexAry: [],
    };
  },
  methods: {
    genRndHex(color) {
      var [h, s, v] = hexToHsl(color);
      var hexAry = [];
      hexAry.push(hslToHex(h, s, v));
      for (let i = 0; i < 6; i++) {
        const new_h = h + 10 - Math.random() * 20;
        const new_s = s + 10 - Math.random() * 40;
        const new_v = v + 10 - Math.random() * 40;

        hexAry.push(hslToHex(new_h, new_s, new_v));
      }

      return hexAry;
    },
  },
  computed: {
    hexAry() {
      return this.genRndHex(this.color);
    },
  },
};
</script>

<style lang="scss">
$size: 80px;
$con-hei: 400px;
.hex-container {
  height: $con-hei;
  position: relative;
  div {
    display: inline-block;
    width: $size;
    height: $size;
    // position: absolute;
    // transform: translate(-50%, -50%);
    // left: 50%;
    // top: 50%;

  }
}
</style>