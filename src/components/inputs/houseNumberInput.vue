<template>
  <div>
    <label for="zipcode">Enter your house number</label>
    <input id="zipcode" @change="zip" maxlength="6" type="text" v-model="houseNumber">
    <div v-if="zipCode.length === 6">{{this.zipCodeValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberInput extends Vue {
  houseNumber = ''

  zip(event: any): void {
    if (/^\d+$/.test(this.zipCode)) {
      this.zipCodeValidator = 'zip code is valid';
      this.$emit('zipCode', this.zipCode);
    } else {
      this.zipCodeValidator = ' zip code is Invalid';
    }
  }
}
</script>

<style scoped>

</style>
