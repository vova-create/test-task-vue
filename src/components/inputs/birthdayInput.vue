<template>
  <div class="birthday-input">
    <label for="birthdayDate">Enter your birthday date</label>
    <input :class="{'birthday-input__input-error':freeYearsValidator || birthdayValidator, 'birthday-input__input-accept': birthdayAccepted}" id="birthdayDate" type="date" @change="birthdayValidate" v-model="birthday">
    <div class="birthday-input__error-text" v-if="birthdayValidator">{{birthdayValidator}}</div>
    <br>
    <label for="freeYears">Claim Free years</label>
    <select @change="birthdayValidate" id="freeYears" v-model="selectedOption">
      <option
        v-for="option in options"
        :key="option"
        :value="option">
        {{ option }}
      </option>
    </select>
    <div class="birthday-input__error-text" v-if="freeYearsValidator">{{this.freeYearsValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class BirthdayInput extends Vue {
  birthday = ''

  birthdayAccepted = false

  birthdayValidator =''

  selectedOption = ''

  freeYearsValidator = ''

  options = [] as number[]

  birthdayValidate(event: any): void {
    const currentYear = new Date().getFullYear();
    const chosenYear = new Date(this.birthday).getFullYear();
    const userAge = (chosenYear - currentYear) * -1;
    if (userAge > 100) {
      this.birthdayValidator = 'You  can not be more then 100 years old';
      this.birthdayAccepted = false;
    } else {
      this.birthdayValidator = '';
      this.freeYearsValidator = '';
      this.birthdayAccepted = true;
      this.$emit('birthday', { birthday: this.birthday });
    }
    const maxYears = userAge - 18;
    if (maxYears < -5) {
      this.birthdayAccepted = false;
      this.freeYearsValidator = 'You must be at least 18 years old';
    } else {
      for (let i = -5; i <= maxYears; i++) {
        this.options.push(i);
      }
    }
    this.$emit('selectedFreeYear', { freeyear: this.selectedOption });
  }
}
</script>

<style scoped>

.birthday-input__input-error{
  border: 2px solid #ff1500;
}

.birthday-input__input-accept{
  border: 2px solid #008000FF;
}

.birthday-input__error-text {
  font-size: 12px;
  color: #ff1500;
}
</style>
