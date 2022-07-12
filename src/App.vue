<template>
  <v-app>
    <v-main>
      <div class="myheader text-h5 text-center mb-4 py-5 font-weight-bold">
        Color Palette Builder
      </div>
      <v-container>
        <div class="d-flex justify-space-around">
          <Picker :id="1" :pickColor="color_1" @color="getColor" />
          <Picker :id="2" :pickColor="color_2" @color="getColor" />
        </div>
        <div class="pt-4">
          <Palette :color="color_1" :ary="genAry_1" />
          <Palette :color="color_2" :ary="genAry_2" />
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Picker from "./components/Picker.vue";
import Palette from "./components/Palette.vue";
import hexToHsl from "hex-to-hsl";
import hslToHex from "hsl-to-hex";

export default {
  name: "App",

  components: { Picker, Palette },

  data: () => ({
    color_1: "#5900ff",
    color_2: "#ff7300",
    colorAry_1: [],
    colorAry_2: []
  }),
  methods: {
    getColor(color, id) {
      if (id == 1) {
        this.color_1 = color;
        this.colorAry_1 = [];
      } else {
        this.color_2 = color;
        this.colorAry_2 = [];
      }
    },
    genAry(color, ary) {
      var [h, s, l] = hexToHsl(color);
      const num = 10
      for (let i = 0; i < num-1; i++) {
        let step = 100 / num;
        ary.push(hslToHex(h, s, step * (num-1 - i)));
      }
      return ary;
    },
  },
  computed: {
    genAry_1() {
      return this.genAry(this.color_1, this.colorAry_1);
    },
    genAry_2() {
      return this.genAry(this.color_2, this.colorAry_2);
    },
  },
};
</script>

<style lang="scss">
.myheader {
  background-color: #eee;
  color: #555;
}
</style>>

