<template>
  <div>
    <label for="houseNumber">Enter your house number</label>
    <input id="houseNumber" @change="houseNumberValidate" type="text" v-model="houseNumber">
    <div>{{this.houseValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberInput extends Vue {
  houseNumber = ''

  houseValidator =''

  houseNumberValidate(event: any): void {
    if (/^\d+$/.test(this.houseNumber)) {
      this.houseValidator = 'zip code is valid';
      this.$emit('houseNumber', `housenumber=${this.houseNumber}`);
    } else {
      this.houseValidator = ' house number is Invalid';
    }
  }
}
</script>

<style scoped>

</style>
