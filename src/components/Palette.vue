<template>
  <div class="palette-container">
    <div
      v-for="(item, index) in lightAry"
      :key="index"
      class="singlePalette"
      :style="{ background: item }"
      v-ripple
      @click="sendOut(item, id)"
    ></div>
  </div>
</template>

<script>
import convert from "color-convert";

export default {
  props: ["id", "color"],
  data() {
    return {};
  },
  methods: {
    sendOut(outcolor, outid) {
      this.$emit("result", outcolor, outid);
    },
    genLightAry(color) {
      var [h, s, v] = convert.hex.hsl(color);
      var ary = [];
      const num = 10;
      const halfNum = num / 2;

      const stepUp = (100 - v) / halfNum;
      const stepDown = (v - 0) / halfNum;

      const evenStep = stepUp < stepDown ? stepUp : stepDown;

      // center pt and upward
      for (let i = 0; i < halfNum; i++) {
        ary.push("#" + convert.hsl.hex(h, s, v + evenStep * i).toLowerCase());
      }
      // reverse ary
      ary.reverse();
      // below center pt and downward
      for (let i = 1; i < halfNum; i++) {
        ary.push("#" + convert.hsl.hex(h, s, v - evenStep * i).toLowerCase());
      }

      return ary;
    },
  },
  computed: {
    lightAry() {
      return this.genLightAry(this.color);
    },
  },
};
</script>

<style lang="scss">
$palette-dia: 80px;
.palette-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding-bottom: 8px;
  @media (max-width: 830px) {
    max-width: 300px;
    margin: auto;
  }
}
.singlePalette {
  width: $palette-dia;
  height: $palette-dia;
  border-radius: $palette-dia;
  cursor: pointer;
  margin-top: 8px;
}
</style>