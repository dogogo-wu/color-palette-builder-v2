<template>
  <v-app>
    <header
      class="myheader py-5"
      :class="$vuetify.theme.dark ? 'mydark' : 'mylight'"
    >
      <div class="text-h5 text-center font-weight-bold">
        Color Palette for Design
      </div>
      <div class="switch-group">
        <v-switch
          v-model="$vuetify.theme.dark"
          inset
          label=""
          hide-details
          class="btn-switch ma-0 pa-0"
        ></v-switch>
        <v-icon @click="$vuetify.theme.dark = !$vuetify.theme.dark"
          >mdi-weather-night</v-icon
        >
      </div>
      <div class="add-btn-dec">
        <v-fab-transition>
          <v-tooltip right>
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                v-show="!add"
                color="blue"
                fab
                dark
                x-small
                outlined
                @click="handleDelClick"
                class="mybtn"
                v-bind="attrs"
                v-on="on"
              >
                <v-icon>mdi-minus</v-icon>
              </v-btn>
            </template>
            <span>Remove 3rd Color</span>
          </v-tooltip>
        </v-fab-transition>
        <v-fab-transition>
          <v-tooltip right>
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                v-show="add"
                color="green"
                fab
                dark
                x-small
                outlined
                @click="handleAddClick"
                class="mybtn"
                v-bind="attrs"
                v-on="on"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </template>
            <span>Add 3rd Color</span>
          </v-tooltip>
        </v-fab-transition>
      </div>
    </header>
    <v-main>
      <v-container>
        <div class="d-flex justify-space-around flex-wrap">
          <Picker
            v-for="item in myobj"
            :key="item.id"
            :id="item.id"
            :color="item.color"
            @color="getColor"
            :iter="iter"
          />
        </div>
        <div class="pt-2">
          <div class="text-h6 text-center">Lightness Variation</div>
          <div class="text-center mb-2">(Click Colors)</div>
          <div class="palette-group">
            <Palette
              v-for="item in myobj"
              :key="item.id"
              :id="item.id"
              :color="item.color"
              @result="getResult"
            />
          </div>
        </div>

        <section class="out-sec">
          <div
            class="out-area pt-3 px-4"
            :class="$vuetify.theme.dark ? 'border-dark' : 'border-light'"
          >
            <div class="text-h6 text-center">Your Design Colors</div>
            <v-tooltip right>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  icon
                  color="green"
                  class="iter-btn"
                  @click="handleIterClick"
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon>mdi-cached</v-icon>
                </v-btn>
              </template>
              <span>Iterate Colors</span>
            </v-tooltip>

            <div class="output mb-5">
              <OutColor
                v-for="item in myobj"
                :key="item.id"
                :bg="item.output"
              />
            </div>
          </div>
        </section>

        <div class="">
          <div class="text-h6 text-center">Similar Colors</div>
          <div class="text-center">(Randomly Generated)</div>
          <div class="hexcolor pb-4">
            <RndHex
              v-for="item in myobj"
              :key="item.id"
              :id="item.id"
              :color="item.color"
              @result="getResult"
              :iter="iter"
            />
          </div>
        </div>
      </v-container>
    </v-main>
    <footer>
      <div class="myfooter" :class="$vuetify.theme.dark ? 'mydark' : 'mylight'">
        <p>Copyright © {{ new Date().getFullYear() }} Leon Wu.&ensp;</p>
        <p>All rights reserved.</p>
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
        color: "#9900ff",
        output: "#ccc",
      },
      {
        id: 2,
        color: "#ff9900",
        output: "#ccc",
      },
    ],
    tmpobj: {
      id: 3,
      color: "#55d3c6",
      output: "#ccc",
    },
    add: true,
    iter: 0,
  }),
  methods: {
    getColor(color, id) {
      this.myobj[id - 1].color = color;
    },
    getResult(outcome, id) {
      this.myobj[id - 1].output = outcome;
    },
    handleAddClick() {
      this.myobj.push(this.tmpobj);
      this.add = !this.add;
    },
    handleDelClick() {
      this.tmpobj.color = this.myobj[2].color;
      this.tmpobj.output = this.myobj[2].output;

      this.myobj.pop();
      this.add = !this.add;
    },
    handleIterClick() {
      this.myobj.forEach((item) => {
        item.color = item.output;
      });
      this.iter = this.iter + 1;
    },
  },
};
</script>

<style>
html,
body {
  width: 100%;
  height: 100%;
  margin: 0px;
  padding: 0px;
  overflow-x: hidden;
}
.myheader {
  position: relative;
}
.switch-group {
  position: absolute;
  margin: 0;
  right: 20px;
  top: 24px;
  display: flex;
  align-items: center;
}
.mybtn {
  position: absolute;
  left: 20px;
  top: 20px;
  border-width: 2px;
}
@media (max-width: 500px) {
  .btn-switch {
    display: none;
  }
  .switch-group {
    right: 10px;
  }
  .mybtn {
    left: 10px;
  }
}
@media (max-width: 350px) {
  .switch-group {
    right: 5px;
  }
  .mybtn {
    left: 5px;
  }
}
.mylight {
  background-color: #eee;
  color: #555;
}
.mydark {
  background-color: #333;
  color: #eee;
}

@media (max-width: 830px) {
  .palette-group {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
}
.out-sec {
  display: flex;
  justify-content: center;
  /* position: fixed;
  right: 10px;
  bottom: 20px; */
}
.out-area {
  border-radius: 1rem;
  border: 2px solid;
  display: inline-block;
  margin: 1rem auto;
  position: relative;
}
.iter-btn {
  position: absolute;
  right: 5px;
  top: 5px;
}
.border-light {
  border-color: #ccc;
}
.border-dark {
  border-color: #777;
}
.output {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.hexcolor {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.myfooter {
  text-align: center;
  padding: 1.5rem;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.myfooter p {
  margin: 0;
}
</style>>

