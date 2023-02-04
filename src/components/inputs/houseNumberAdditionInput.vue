<template>
  <div>
    <label for="houseNumber">Enter your additional house number</label>
    <input
      id="houseNumber"
      @change="houseNumberAdditionalValidate"
      type="text"
      v-model="houseNumberAdditional">
    <div>{{this.houseValidatorAdditional }}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberAdditionInput extends Vue {
  houseNumberAdditional = ''

  houseValidatorAdditional =''

  houseNumberAdditionalValidate(event: any): void {
    if (/^[a-zA-Z0-9]+$/.test(this.houseNumberAdditional)) {
      this.houseValidatorAdditional = 'zip code is valid';
      this.$emit('houseAdditional', { houseadditional: this.houseNumberAdditional });
    } else {
      this.houseValidatorAdditional = 'Additional house number is Invalid';
    }
  }
}
</script>

<style scoped>

</style>
