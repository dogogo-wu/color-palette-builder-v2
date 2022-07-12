<template>
  <v-app>
    <v-main>
      <div class="myheader text-h4 text-center mb-2 py-5 font-weight-bold">
        Color Palette Builder
      </div>
      <v-container>
        <div>
          <!-- <Picker :pickColor="color_1" /> -->
          <p>Pick a base color!</p>
          <input
            class="mypicker"
            type="color"
            name="favcolor"
            v-model="color_1"
          />
          <v-text-field
            v-model="color_1"
          ></v-text-field>
          <!-- <div class="mycir rounded-circle" :style="{backgroundColor: color_1}"></div>
          <v-color-picker
            dot-size="25"
            mode="hex"
            elevation="15"
            v-model="color_1"
          ></v-color-picker> -->
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
// import Picker from "./components/Picker.vue"
export default {
  name: "App",

  components: {},

  data: () => ({
    color_1: "#ff0000",
  }),
};
</script>

<style lang="scss">
.myheader {
  background-color: #eee;
  color: #555;
}
.mycir {
  width: 100px;
  height: 100px;
}
.mypicker {
  width: 100px;
  height: 100px;
  border-radius: 50px;
  border: none;
  cursor: pointer;

  &::-webkit-color-swatch {
    border-radius: 50px;
    border: none;
  }
  &::-moz-color-swatch {
    border-radius: 50px;
    border: none;
  }
}
</style>>

