<template>
  <select @change="kilometrageToSelect" id="freeYears" v-model="kilometrageSelected">
    <option
      v-for="option in kilometrageOption "
      :key="option"
      :value="option">
      {{ option }}
    </option>
  </select>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class KilometrageInput extends Vue {
  kilometrageSelected = ''
  kilometrageOption = [
    '0 t/m 7500 KM',
    '7501 t/m 10000 KM',
    '10001 t/m 12000 KM',
    '12001 t/m 15000 KM',
    '15000 t/m 20000 KM',
    '20001 t/m 25000 KM',
    '25001 t/m 30000 KM',
    '30001 t/m 90000 KM',
  ] as any

  houseValidatorAdditional =''

  kilometrageToSelect(event: any): void {
    console.log(this.kilometrageSelected);
  }
}
</script>

<style scoped>

</style>
