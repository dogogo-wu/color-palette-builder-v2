<template>
  <v-tooltip bottom>
    <template v-slot:activator="{ on, attrs }">
      <v-btn
        class="outcir"
        :style="{ background: bg }"
        v-bind="attrs"
        v-on="on"
        fab
        elevation="0"
        plain
        width="80px"
        height="80px"
        :data-clipboard-text="bg"
      ></v-btn>
    </template>
    <span>Copy Color (HEX)</span>
  </v-tooltip>
</template>

<script>
import Clipboard from 'clipboard';

export default {
  props: ["bg"],
  mounted () {
    new Clipboard( ".outcir" );
  },
};
</script>

<style lang="scss">
$out-cir-dia: 80px;
.outcir {
  width: $out-cir-dia;
  height: $out-cir-dia;
  border-radius: $out-cir-dia;
  border: none;
  cursor: pointer;

  display: inline-block;
  margin: 1rem;
}
</style>