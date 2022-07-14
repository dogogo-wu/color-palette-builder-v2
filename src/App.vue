<template>
  <v-app>
    <header class="myheader text-h5 text-center mb-4 py-5 font-weight-bold">
      Color Palette Builder
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
          <div class="out-area pt-3">
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
      <div class="myfooter">
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
      // {
      //   id: 3,
      //   color: "#ff73ff",
      //   output: "#ccc",
      // },
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
  background-color: #eee;
  color: #555;
}
.out-area {
  border-radius: 1rem;
  border: 2px solid #ccc;
  display: inline-block;
  margin: 1rem auto;
}
.output {
  display: inline-block;
}
.hexcolor {
  display: flex;
  justify-content: space-around;
}
.myfooter {
  color: #555;
  background: #eee;
  text-align: center;
  padding: 1.5rem;
}
</style>>

