<template>
  <div class="palette-container">
    <!-- <div v-if="colorAry.length">
        <div v-for="item in colorAry" :key="item" class="singlePalette" :style="{ background: item }"></div>
    </div> -->
    <div v-for="item in ary" :key="item" class="singlePalette" :style="{ background: item }"></div>
    <!-- <div class="singlePalette" :style="{ background: color }"></div> -->
  </div>
</template>

<script>

export default {
    props: ['color', 'ary'],
    data() {
        return {
            // colorAry: [],
        }
    },
    mounted () {
        console.log("mounted");

    },
}

</script>

<style lang="scss">
$palette-dia: 80px;
.palette-container {
  display: flex;
  justify-content: space-around;
  padding: 1rem 0;
}
.singlePalette {
  width: $palette-dia;
  height: $palette-dia;
  border-radius: $palette-dia;
}
</style>