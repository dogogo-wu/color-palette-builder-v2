<template>
  <v-app>
    <header
      class="myheader mb-4 py-5"
      :class="$vuetify.theme.dark ? 'mydark' : 'mylight'"
    >
      <div class="text-h5 text-center font-weight-bold">
        Color Palette Builder
      </div>
      <div class="switch-group">
        <v-switch
          v-model="$vuetify.theme.dark"
          inset
          label=""
          hide-details
          class="ma-0"
        ></v-switch>
        <v-icon>mdi-weather-night</v-icon>
      </div>
    </header>
    <v-main>
      <v-container>
        <div class="d-flex justify-space-around flex-wrap">
          <Picker
            v-for="item in myobj"
            :key="item.id"
            :id="item.id"
            :pickColor="item.color"
            @color="getColor"
          />
        </div>
        <div class="pt-4">
          <div class="text-h6 text-center">Pick Colors</div>
          <div class="text-center">(Lightness variation)</div>
          <Palette
            v-for="item in myobj"
            :key="item.id"
            :id="item.id"
            :color="item.color"
            @result="getResult"
          />
        </div>

        <div class="d-flex justify-center">
          <div
            class="out-area pt-3 px-4"
            :class="$vuetify.theme.dark ? 'border-dark' : 'border-light'"
          >
            <div class="text-h6 text-center">Your Color</div>
            <div class="output mb-5">
              <OutColor
                v-for="item in myobj"
                :key="item.id"
                :bg="item.output"
              />
            </div>
          </div>
        </div>

        <div class="pt-4">
          <div class="text-h6 text-center">Similar Random Colors</div>
          <div class="hexcolor">
            <RndHex
              v-for="item in myobj"
              :key="item.id"
              :id="item.id"
              :color="item.color"
              @result="getResult"
            />
          </div>
        </div>
      </v-container>
    </v-main>
    <footer>
      <div class="myfooter" :class="$vuetify.theme.dark ? 'mydark' : 'mylight'">
        Copyright © {{ new Date().getFullYear() }} Leon Wu. All rights reserved.
      </div>
    </footer>
  </v-app>
</template>

<script>
import Picker from "./components/Picker.vue";
import Palette from "./components/Palette.vue";
import OutColor from "./components/OutColor.vue";
import RndHex from "./components/RndHex.vue";

export default {
  name: "App",

  components: { Picker, Palette, OutColor, RndHex },

  data: () => ({
    myobj: [
      {
        id: 1,
        color: "#5900ff",
        output: "#ccc",
      },
      {
        id: 2,
        color: "#ff7300",
        output: "#ccc",
      },
    ],
  }),
  methods: {
    getColor(color, id) {
      this.myobj[id - 1].color = color;
    },
    getResult(outcome, id) {
      this.myobj[id - 1].output = outcome;
    },
  },
};
</script>

<style>
.myheader {
  position: relative;
}
.switch-group {
  position: absolute;
  margin: 0;
  right: 20px;
  top: 20px;
  display: flex;
  align-items: center;
}
.mylight {
  background-color: #eee;
  color: #555;
}
.mydark {
  background-color: #333;
  color: #eee;
}
.out-area {
  border-radius: 1rem;
  border: 2px solid;
  display: inline-block;
  margin: 1rem auto;
}
.border-light {
  border-color: #ccc;
}
.border-dark {
  border-color: #777;
}
.output {
  display: inline-block;
}
.hexcolor {
  display: flex;
  justify-content: space-around;
}
.myfooter {
  text-align: center;
  padding: 1.5rem;
}
</style>>

