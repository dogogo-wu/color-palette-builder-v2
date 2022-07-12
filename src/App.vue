<template>
  <v-app>
    <v-main>
      <div class="myheader text-h4 text-center mb-2 py-5 font-weight-bold">
        Color Palette Builder
      </div>
      <v-container>
        <div>
          <Picker :id="1" :pickColor="color_1" @color='getColor'/>
          <Picker :id="2" :pickColor="color_2" @color='getColor'/>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Picker from "./components/Picker.vue";
export default {
  name: "App",

  components: {Picker},

  data: () => ({
    color_1: "#ff0000",
    color_2: "#ff00ff"
  }),
  methods: {
    getColor(color, id) {
      if (id == 1) {
        this.color_1 = color;
      }else{
        this.color_2 = color;
      }
      
    }
  },
};
</script>

<style lang="scss">
.myheader {
  background-color: #eee;
  color: #555;
}
</style>>

