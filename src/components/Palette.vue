<template>
  <div class="palette-container">
    <div v-for="(item, index) in ary" :key="index" class="singlePalette" :style="{ background: item }" @click="sendOut(item, id)"></div>
  </div>
</template>

<script>

export default {
    props: ['id', 'ary'],
    data() {
        return {
            
        }
    },
    methods: {
      sendOut(outcolor, outid) {
        this.$emit('result', outcolor, outid)
      }
    },
}

</script>

<style lang="scss">
$palette-dia: 80px;
.palette-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 1rem 0;
}
.singlePalette {
  width: $palette-dia;
  height: $palette-dia;
  border-radius: $palette-dia;
  cursor: pointer;
}
</style>