<template>
  <div class="licence-plate">
    <form @submit.prevent="submit">
      <label class="licence-plate__label" for="licencePlate">Enter your licence Plate</label>
      <input :class="{'licence-plate__input-error':errorMessage, 'licence-plate__input-accept': brand && manufacturingYear}" id="licencePlate" v-model="licensePlate" type="text" />
      <button class="licence-plate__btn" type="submit">get vehicle  information from the license plate</button>
    </form>
    <p  class="licence-plate__error-text" v-if="errorMessage">{{ errorMessage }}</p>
    <p class="licence-plate__licence-info" v-if="brand && manufacturingYear">
      Brand: {{ brand }}<br />
      Manufacturing Year: {{ manufacturingYear }}
    </p>
  </div>
</template>

<script lang="ts" >
import { Options, Vue } from 'vue-class-component';
import axios from 'axios';

interface VehicleData {
  merk: string;
  datum_eerste_toelating: string;
}
@Options({
  components: {
  },
})
export default class LicensePlateInput extends Vue {
  licensePlate = '';

  brand = '';

  manufacturingYear = '';

  errorMessage = '';

  async submit() {
    try {
      const res = await axios.get(`https://opendata.rdw.nl/resource/m9d7-ebf2.json?kenteken=${this.licensePlate}`);
      const data = res.data as VehicleData[];
      if (this.licensePlate !== this.licensePlate.replace(/-/g, '').toUpperCase()) {
        this.errorMessage = 'Invalid license plate.';
        return;
      }
      this.brand = data[0].merk;
      this.manufacturingYear = data[0].datum_eerste_toelating;
      this.$emit('brandAndYear', { brand: this.brand, manufacturingyear: this.manufacturingYear });

      this.errorMessage = '';
    } catch (error) {
      this.manufacturingYear = '';
      this.errorMessage = '';
      this.errorMessage = 'An error occurred while retrieving the information.';
    }
  }
}
</script>

<style scoped>

.licence-plate__btn {
  padding: 6px 12px;
  border: 1px solid #008000FF;
  border-radius: 5px;
  background-color: #008000FF;
  color: #FFFFFFFF;
  font-size: 12px;
  cursor: pointer;
  margin-bottom: 10px;
}

.licence-plate__licence-info {
  background-color: #A0EF7CFF;
}
.licence-plate__error-text {
  font-size: 12px;
  color: #ff1500;
}

.licence-plate__input-error{
  border: 2px solid #ff1500;
}

.licence-plate__input-accept{
  border: 2px solid #008000FF;
}

</style>
