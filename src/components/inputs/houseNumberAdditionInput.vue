<template>
  <div class="additional-house">
    <label for="houseNumber">Enter your additional house number</label>
    <input
      id="houseNumber"
      @change="houseNumberAdditionalValidate"
      type="text"
      :class="{'additional-house__input-accept': houseNumberAdditional,}"
      v-model="houseNumberAdditional">
    <div class="additional-house__error-text">{{houseAdditionalInvalid  }}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class HouseNumberAdditionInput extends Vue {
  houseNumberAdditional = ''

  houseNumberAdditionalValidate(event: any): void {
    if (/^[a-zA-Z0-9]+$/.test(this.houseNumberAdditional)) {
      this.$emit('houseAdditional', { houseadditional: this.houseNumberAdditional });
    }
  }
}
</script>

<style scoped>
.additional-house__input-accept{
  border: 2px solid #008000FF;
}

</style>
