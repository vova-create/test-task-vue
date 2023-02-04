<template>
  <div class="house-number">
    <label for="houseNumber">Enter your house number</label>
    <input :class="{'house-number__input-accept':houseNumber }" id="houseNumber" @change="houseNumberValidate" type="number" v-model="houseNumber">
    <div>{{houseValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberInput extends Vue {
  houseNumber = ''

  houseValidator =''

  houseNumberValidate(event: any): void {
    this.$emit('houseNumber', { housenumber: this.houseNumber });
  }
}
</script>

<style scoped>
.house-number__input-accept{
  border: 2px solid #008000FF;
}

</style>
