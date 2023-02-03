<template>
  <div>
    <form @submit.prevent="submit">
      <label for="licencePlate">Enter your licence Plate</label>
      <input id="licencePlate" v-model="licensePlate" type="text" />
      <button type="submit">get vehicle  information from the license plate</button>
    </form>
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <p v-if="brand && manufacturingYear">
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
      console.log(this.licensePlate);
      const res = await axios.get(`https://opendata.rdw.nl/resource/m9d7-ebf2.json?kenteken=${this.licensePlate}`);
      const data = res.data as VehicleData[];
      if (this.licensePlate !== this.licensePlate.replace(/-/g, '').toUpperCase()) {
        this.errorMessage = 'Invalid license plate.';
        return;
      }
      this.brand = data[0].merk;
      this.manufacturingYear = data[0].datum_eerste_toelating;
      this.$emit('brandAndYear', this.brand, this.manufacturingYear);
      this.errorMessage = '';
    } catch (error) {
      this.errorMessage = 'An error occurred while retrieving the information.';
    }
  }
}
</script>

<style scoped>

</style>
