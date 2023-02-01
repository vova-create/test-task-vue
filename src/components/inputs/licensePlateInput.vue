<template>
  <div>
    <form @submit.prevent="submit">
      <input v-model="licensePlate" type="text" />
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
      const response = await fetch(`https://opendata.rdw.nl/resource/m9d7-ebf2.json?kenteken=${this.licensePlate}`);
      const data = (await response.json()) as VehicleData[];

      if (!data.length) {
        this.errorMessage = 'Invalid license plate.';
        return;
      }

      this.brand = data[0].merk;
      this.manufacturingYear = data[0].datum_eerste_toelating;
      this.errorMessage = '';
      console.log(this.manufacturingYear);
      console.log(this.brand);
    } catch (error) {
      this.errorMessage = 'An error occurred while retrieving the information.';
    }
  }
}
</script>

<style scoped>

</style>
