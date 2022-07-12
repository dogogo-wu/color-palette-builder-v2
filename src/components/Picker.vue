<template>
  <div>
    <p>Pick a base color!</p>
    <input class="mypicker" type="color" v-model="mycolor" @change="passColor"/>
    <v-text-field v-model="mycolor" @change="passColor"></v-text-field>
  </div>
</template>

<script>
export default {
    props: ['pickColor', 'id'],
    data() {
        return {
            mycolor: this.pickColor
        }
    },
    methods: {
        passColor() {
            this.$emit('color', this.mycolor, this.id)
        }
    },
};
</script>

<style lang="scss">
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
</style>