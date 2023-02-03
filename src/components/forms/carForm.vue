<template>
  <simple-card class="vd-form">
    <template #title>Autoverzekering vergelijken</template>

    <template #content>
          <license-plate-input @brandAndYear="getCarInfo"/>
          <zip-code-input @zip-code="getCarInfo"/>
          <house-number-input @house-number="getCarInfo"/>
         <house-number-addition-input @house-additional="getCarInfo"/>
        <birthday-input @selected-free-year="getCarInfo" @birthday="getCarInfo"/>
       <!-- LicensePlate -->

        <!-- Zipcode -->

        <!-- Housenumber -->

        <!-- Housenumber addition -->

        <!-- birthdate -->

        <!-- ClaimFree years -->

        <!-- Kilometrage -->

        <div class="btn" @click="onSubmit">
            Vergelijken
        </div>
    </template>
  </simple-card>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import LicensePlateInput from '@/components/inputs/licensePlateInput.vue';
import ZipCodeInput from '@/components/inputs/zipCodeInput.vue';
import HouseNumberInput from '@/components/inputs/houseNumberInput.vue';
import BirthdayInput from '@/components/inputs/birthdayInput.vue';
import SimpleCard from './simpleCard.vue';
import HouseNumberAdditionInput from '@/components/inputs/houseNumberAdditionInput.vue';


@Options({
  components: {
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

  onSubmit(): void {
    console.log('Button is clicked');
  }

  getCarInfo(...args: string[]): void {
    this.formArray = this.formArray.concat(args);
    const some = this.formArray.join('&');
    console.log(some);
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
