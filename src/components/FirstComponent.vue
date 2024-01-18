<template>
  <div class="loan-form">
    <LoanCarousel />

    <!-- Form starts here -->
    <form @submit.prevent="submitForm">
      <!-- User information display -->
      <UserInfoAccordion />

      <!-- Personal information section -->
      <div class="mb-3">
        <label>Personal Information</label><br>
        <label for="country" class="form-label">Country</label>
        <select id="country" class="form-select" v-model="formData.country">
          <option selected>Choose...</option>
          <!-- Populate with actual country options -->
        </select>
      </div>

      <div class="row g-3 mb-3">
        <div class="col-md">
          <label for="city" class="form-label">City / Parish</label>
          <input type="text" id="city" class="form-control" v-model="formData.city">
        </div>
        <div class="col-md">
          <label for="county" class="form-label">County</label>
          <input type="text" id="county" class="form-control" v-model="formData.county">
        </div>
      </div>

      <div class="row g-3 mb-3">
        <div class="col-md">
          <label for="street" class="form-label">Street</label>
          <input type="text" id="street" class="form-control" v-model="formData.street">
        </div>

        <div class="col-md-4">
          <label for="house" class="form-label">House</label>
          <input type="text" id="house" class="form-control" v-model="formData.house">
        </div>

        <div class="col-md-4">
          <label for="apartment" class="form-label">Apartment</label>
          <input type="text" id="apartment" class="form-control" v-model="formData.apartment">
        </div>
        <div class="col-md-4">
          <label for="postalCode" class="form-label">Postal Code</label>
          <input type="text" id="postalCode" class="form-control" v-model="formData.postalCode">
        </div>
      </div>

      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="manualAddress" v-model="formData.manualAddress">
        <label class="form-check-label" for="manualAddress">Add address manually</label>
      </div>

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
import LoanCarousel from './LoanCarousel.vue'
import UserInfoAccordion from './UserInfoAccordion.vue'
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

</script>

<style scoped>
.loan-form {
  max-width: 764px;
}

</style>

