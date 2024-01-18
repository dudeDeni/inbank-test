<template>
  <div class="loan-form">
    <!-- Form starts here -->
    <form @submit.prevent="submitForm">
      <LoanCarousel />
      <!-- User information display -->
      <UserInfoAccordion />

      <!-- Personal information section -->
      <label>Personal Information</label><br>
      

      <CheckboxManual @check-manually="toggleManualFields"/>

      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="pepCheck" v-model="formData.pepCheck">
        <label class="form-check-label" for="pepCheck">Neither I nor my family member is PEP</label>
      </div>

      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="beneficiaryCheck" v-model="formData.beneficiaryCheck">
        <label class="form-check-label" for="beneficiaryCheck">I'm the ultimate beneficiary</label>
      </div>

      <div class="d-grid gap-2">
        <button type="submit" class="btn btn-primary">Continue</button>
      </div>
    </form>

  </div>
</template>

<script setup>
import CheckboxManual from './CheckboxManual.vue';
import LoanCarousel from './LoanCarousel.vue';
import UserInfoAccordion from './UserInfoAccordion.vue';
import Input from './reusables/Input.vue';
import { ref } from 'vue'

const formData = ref({
  country: '',
  city: '',
  county: '',
  street: '',
  house: '',
  apartment: '',
  postalCode: '',
  manualAddress: '',
  pepCheck: '',
  beneficiaryCheck: ''
})

const isFormManual = ref(false);

const toggleManualFields = (isChecked) => {
  isFormManual.value = isChecked
}

</script>

<style scoped>
.loan-form {
  max-width: 764px;
}

</style>

