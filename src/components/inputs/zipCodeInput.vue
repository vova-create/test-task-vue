<template>
<div>
  <label for="zipcode">Enter your zip code</label>
  <input id="zipcode" @change="zip" maxlength="6" type="text" v-model="zipCode">
  <div v-if="zipCode.length === 6">{{this.zipCodeValidator}}</div>
</div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class ZipCodeInput extends Vue {
  zipCode = ''

  zipCodeValidator = ''

  zip(event: any): void {
    if (/^\d+$/.test(this.zipCode)) {
      this.zipCodeValidator = 'zip code is valid';
      this.$emit('zipCode', `zipcode=${this.zipCode}`);
    } else {
      this.zipCodeValidator = ' zip code is Invalid';
    }
  }
}
</script>

<style scoped>

</style>
