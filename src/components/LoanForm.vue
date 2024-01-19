<template>
  <div class="loan-form">
    <!-- Form starts here -->
    <form @submit.prevent="submitForm">
      <!-- Loan amount and duration -->
      <LoanCarousel />
      <!-- User information display -->
      <UserInfoAccordion />

      <!-- Personal information section -->
      <div class="mb-4 mx-3">Personal Information</div>
      <ManualForm
        v-if="isFormManual"
        :country="formData.country"
        :city="formData.city"
        :county="formData.county"
        :town-ship="formData.townShip"
        :street="formData.street"
        :house="formData.house"
        :apartment="formData.apartment"
        :postal-code="formData.postalCode"
        @update="updateFields($event)"
      />
      <OptionForm 
        v-if="!isFormManual"
        :country="formData.country"
        :city="formData.city"
        :county="formData.county"
        :town-ship="formData.townShip"
        :street="formData.street"
        :house="formData.house"
        :apartment="formData.apartment"
        :postal-code="formData.postalCode"
        :cities="cities"
        :counties="counties"
        :towns="towns"
        @update="updateFields($event)"
      />

      <CheckboxManual @check-manually="toggleManualFields"/>

      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="pepCheck" v-model="formData.pepCheck">
        <label class="form-check-label" for="pepCheck">Neither I nor my family member is PEP</label>
      </div>

      <div class="mb-3 form-check">
        <input type="checkbox" class="" id="beneficiaryCheck" v-model="formData.beneficiaryCheck">
        <label class="form-check-label" for="beneficiaryCheck">I'm the ultimate beneficiary</label>
      </div>

      <div class="row justify-content-center">
        <button type="submit" class="btn btn-primary col-6">Continue</button>
      </div>
    </form>

  </div>
</template>

<script setup>
import CheckboxManual from './CheckboxManual.vue';
import LoanCarousel from './LoanCarousel.vue';
import UserInfoAccordion from './UserInfoAccordion.vue';
import ManualForm from './forms/ManualForm.vue';
import { ref } from 'vue'
import OptionForm from './forms/OptionForm.vue';


const formData = ref({
  country: 'World',
  city: null,
  county: null,
  townShip: null,
  street: null,
  house: null,
  apartment: null,
  postalCode: null,
  pepCheck: null,
  beneficiaryCheck: null
})

const cities = ref(['Tallinn', 'Tartu', 'Pärnu', 'Rapla', 'Jõhvi'])
const counties = ref(['Harjumaa', 'Ida-Virumaa', 'Põlvamaa', 'Järvamaa', 'Jõgevamaa', 'Saaremaa'])
const towns = ref(['Keila', 'Kalamaja', 'Pirita', 'Lasnamäe', 'Nõmme', 'Kakumäe'])

const isFormManual = ref(false);

const toggleManualFields = (isChecked) => {
  isFormManual.value = isChecked
}

const updateFields = (payload) => {
  formData.value[payload.target] = payload.value
}

</script>

<style scoped>
.loan-form {
  max-width: 764px;
  width: 100%;
}

</style>

