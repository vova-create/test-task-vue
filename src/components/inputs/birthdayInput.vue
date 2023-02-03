<template>
  <div>
    <label for="birthdayDate">Enter your birthday date</label>
    <input id="birthdayDate" type="date" @change="birthdayValidate" v-model="birthday">
    <div v-if="birthdayValidator">{{this.birthdayValidator}}</div>
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
    <div v-if="freeYearsValidator">{{this.freeYearsValidator}}</div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class BirthdayInput extends Vue {
  birthday = ''

  birthdayValidator =''

  selectedOption = ''

  freeYearsValidator = ''

  options = [] as number[]

  birthdayValidate(event: any): void {
    if (this.selectedOption) {
      this.$emit('selectedFreeYear', `freeyear=${this.selectedOption}`);
      return;
    }
    const currentYear = new Date().getFullYear();
    const chosenYear = new Date(this.birthday).getFullYear();
    const userAge = (chosenYear - currentYear) * -1;
    if (userAge > 100) {
      this.birthdayValidator = 'You  can not be more then 100 years old';
    } else {
      this.birthdayValidator = '';
      this.$emit('birthday', `birthday=${this.birthday}`);
    }
    const maxYears = userAge - 18;
    if (maxYears < -5) {
      this.freeYearsValidator = 'You must be at least 18 years old';
    } else {
      for (let i = -5; i <= maxYears; i++) {
        this.options.push(i);
      }
    }
  }
}
</script>

<style scoped>

</style>
