<template>
  <div>
    <label for="houseNumber">Enter your house number</label>
    <input id="houseNumber" @change="houseNumberValidate" type="number" v-model="houseNumber">
    <div>{{this.houseValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberInput extends Vue {
  houseNumber = ''

  houseValidator =''

  houseNumberValidate(event: any): void {
    this.houseValidator = 'houseNumber is valid';
    this.$emit('houseNumber', { housenumber: this.houseNumber });
  }
}
</script>

<style scoped>

</style>
