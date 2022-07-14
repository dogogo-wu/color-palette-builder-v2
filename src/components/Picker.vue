<template>
  <div class="picker-container">
    <div class="text-h6 mb-3">Pick base color !</div>
    <input class="mypicker" type="color" v-model="mycolor"  />
    <v-text-field v-model="mycolor" class="picker-text"></v-text-field>
  </div>
</template>

<script>
export default {
  props: ["color", "id"],
  data() {
    return {
      mycolor: this.color,
    };
  },
  updated() {
    this.$emit("color", this.mycolor, this.id);
  },
};
</script>

<style lang="scss">
$cir-dia: 80px;

.picker-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 28px 20px 16px;
  margin-top: 16px;
  border-radius: 1rem;
  border: 1px solid #ddd;

  .picker-text {
    width: $cir-dia;
    input {
      text-align: center;
    }
  }
}
.mypicker {
  width: $cir-dia;
  height: $cir-dia;
  border: none;
  cursor: pointer;
  padding: 0;

  &::-webkit-color-swatch {
    border-radius: $cir-dia;
    border: none;
    padding: 0;
  }
  &::-webkit-color-swatch-wrapper {
    border: none;
    border-radius: 50%;
    padding: 0;
  }
  &::-moz-color-swatch {
    border-radius: $cir-dia;
    border: none;
  }
}
</style>