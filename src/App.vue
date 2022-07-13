<template>
  <v-app>
    <v-main>
      <div class="myheader text-h5 text-center mb-4 py-5 font-weight-bold">
        Color Palette Builder
      </div>
      <v-container>
        <div class="d-flex justify-space-around flex-wrap">
          <Picker :id="obj1.id" :pickColor="obj1.color" @color="getColor" />
          <Picker :id="obj2.id" :pickColor="obj2.color" @color="getColor" />
        </div>
        <div class="pt-4">
          <div class="text-h6 text-center">Pick Output Colors</div>
          <div class="text-center">(Lightness variation)</div>
          <Palette :id="obj1.id" :ary="genAry_1" @result="getResult" />
          <Palette :id="obj2.id" :ary="genAry_2" @result="getResult" />
        </div>
        <div class="pt-4 d-flex flex-column align-center">
          <div class="text-h6 text-center">Output</div>
          <div class="output mb-5">
            <OutColor :bg="obj1.output" />
            <OutColor :bg="obj2.output" />
          </div>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Picker from "./components/Picker.vue";
import Palette from "./components/Palette.vue";
import OutColor from "./components/OutColor.vue";
import hexToHsl from "hex-to-hsl";
import hslToHex from "hsl-to-hex";

export default {
  name: "App",

  components: { Picker, Palette, OutColor },

  data: () => ({
    obj1: {
      id: 1,
      color: "#5900ff",
      paletteAry: [],
      output: "#5900ff",
    },
    obj2: {
      id: 2,
      color: "#ff7300",
      paletteAry: [],
      output: "#ff7300",
    },
  }),
  methods: {
    getColor(color, id) {
      if (id == 1) {
        this.obj1.color = color;
        this.obj1.paletteAry = [];
      } else if (id == 2) {
        this.obj2.color = color;
        this.obj2.paletteAry = [];
      }
    },
    genLAry(color, ary) {
      var [h, s, v] = hexToHsl(color);
      const num = 10;
      const halfNum = num / 2;

      const stepUp = (100 - v) / halfNum;
      const stepDown = (v - 0) / halfNum;

      // center pt and upward
      for (let i = 0; i < halfNum; i++) {
        ary.push(hslToHex(h, s, v + stepUp * i));
      }
      // reverse ary
      ary.reverse();
      // below center pt and downward
      for (let i = 1; i < halfNum; i++) {
        ary.push(hslToHex(h, s, v - stepDown * i));
      }

      return ary;
    },
    getResult(outcome, outid) {
      if (outid == 1) {
        this.obj1.output = outcome;
      } else if (outid == 2) {
        this.obj2.output = outcome;
      }
    },
  },
  computed: {
    genAry_1() {
      return this.genLAry(this.obj1.color, this.obj1.paletteAry);
    },
    genAry_2() {
      return this.genLAry(this.obj2.color, this.obj2.paletteAry);
    },
  },
};
</script>

<style lang="scss">
.myheader {
  background-color: #eee;
  color: #555;
}
.output{
  display: inline-block;
  border-radius: 1rem;
  border: 1px solid #ddd;
}
</style>>

