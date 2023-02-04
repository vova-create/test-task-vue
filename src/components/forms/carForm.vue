<template>
  <simple-card class="vd-form">
    <template #title>Autoverzekering vergelijken</template>

    <template #content>
          <license-plate-input @brandAndYear="onInputChange"/>
          <zip-code-input @zip-code="onInputChange"/>
          <house-number-input @house-number="onInputChange"/>
         <house-number-addition-input @house-additional="onInputChange"/>
        <birthday-input @selected-free-year="onInputChange" @birthday="onInputChange"/>
        <kilometrage-input @kilometrage="onInputChange"/>
        <div class="btn" @click="onSubmit">
            Vergelijken
        </div>
      <div v-if="errorText">{{this.errorText}}</div>
    </template>
  </simple-card>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import LicensePlateInput from '@/components/inputs/licensePlateInput.vue';
import ZipCodeInput from '@/components/inputs/zipCodeInput.vue';
import HouseNumberInput from '@/components/inputs/houseNumberInput.vue';
import BirthdayInput from '@/components/inputs/birthdayInput.vue';
import HouseNumberAdditionInput from '@/components/inputs/houseNumberAdditionInput.vue';
import KilometrageInput from '@/components/inputs/kilometrageInput.vue';
import axios from 'axios';
import SimpleCard from './simpleCard.vue';

@Options({
  components: {
    KilometrageInput,
    HouseNumberAdditionInput,
    BirthdayInput,
    HouseNumberInput,
    ZipCodeInput,
    SimpleCard,
    LicensePlateInput,
  },
})
export default class CarForm extends Vue {
  formArray = [] as string[]

  formData = {

  }

  errorText = ''

  onSubmit(): void {
    const urlParams = Object.entries(this.formData).map(([key, value]) => `${key}=${value}`).join('&');
    axios.post(`https://en.wikipedia.org/wiki/${urlParams}`)
      .then((response) => {
        alert(response.data);
      })
      .catch((error) => {
        alert(error);
      });
  }

  onInputChange(data: {[key:string]:string}) {
    this.formData = { ...this.formData, ...data };
  }
}
</script>

<style scoped>
    .vd-form {
        width: 330px;
    }

    @media only screen and (max-width: 768px) {
        .vd-form {
            width: 100%;
        }
    }

    .btn {
        background: #0cbe3b;
        text-align: center;
        padding: 10px 10px;
        font-weight: 600;
        color: white;
        border-radius: 4px;
        cursor: pointer;
        transition: .1s ease;
    }

    .btn:hover {
        background: #0ed642;
    }
</style>
