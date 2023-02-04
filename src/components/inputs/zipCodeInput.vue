<template>
<div class="zipcode">
  <label for="zipcode">Enter your zip code</label>
  <input  :class="{'zipcode__input-error':zipCodeValidatorInvalid, 'zipcode__input-accept':zipCodeValidatorValid }" id="zipcode" @change="zipCodeValidate" maxlength="6" type="text" v-model="zipCode">
  <div class="zipcode__error-text">{{zipCodeValidatorInvalid }}</div>
</div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class ZipCodeInput extends Vue {
  zipCode = ''

  zipCodeValidatorValid = false

  zipCodeValidatorInvalid = ''

  zipCodeValidate(event: Event): void {
    if (this.zipCode === this.zipCode.trim().toUpperCase() && this.zipCode.length === 6) {
      this.zipCodeValidatorValid = true;
      this.zipCodeValidatorInvalid = '';
      this.$emit('zipCode', { zipcode: this.zipCode });
    } else {
      this.zipCodeValidatorInvalid = ' zip code is invalid';
      this.zipCodeValidatorValid = false;

    }
  }
}
</script>

<style scoped>

.zipcode__input-error{
  border: 2px solid #ff1500;
}

.zipcode__input-accept{
  border: 2px solid #008000FF;
}

.zipcode__error-text {
  font-size: 12px;
  color: #ff1500;
}
</style>
