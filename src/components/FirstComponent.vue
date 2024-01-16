<template>
  <div class="loan-form">
    <!-- Carusel for the loan -->
    <div id="carousel1" class="carousel slide mb-4" data-bs-touch="false">
      <div class="bg-primary text-textWhite rounded-pill py-2 gx-2 d-flex" style="height: 54px;">
        <div class="carousel-inner">
          <div class="carousel-item ">
            <button class="carousel-control-prev" type="button" data-bs-target="#carousel1" data-bs-slide="prev">
              <!-- <img src="../assets/arrow.svg" height="13" width="6"/> -->
              <span class="carousel-control-prev-icon" aria-hidden="true" style="height: 13px;"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <div class="row align-items-center m-0 px-0">
              <div class="col-6 d-flex justify-content-end">
                <label class="fw-light lh-lg fs-5">Your loan application</label>
              </div>
              <div class="col">
                <div class="fw-lighter" style="margin-top: 2px;">2700€ / 36<span class="fs-6">&nbsp;months</span></div>
              </div>
            </div>
            
          </div>
  
          <div class="carousel-item active" style="height: 40px;">
            <div class="row align-items-center text-left m-0 px-0" style="height: 40px;">
              <div class="col">
                <div class="fw-light lh-base fs-6">Amount</div>
              </div>
              <div class="col">
                <label class="fw-light lh-base fs-6">Duration</label>
              </div>
              <div class="col">
                <label class="fw-light lh-base fs-6">Monthly Payment</label>
              </div>
            </div>

            <button class="col carousel-control-next" type="button" data-bs-target="#carousel1" data-bs-slide="next">
              <div class="bg-white rounded-pill" style="height: 2rem;">
                <span class="carousel-control-next-icon" aria-hidden="true" style="height: 15px;margin-top: 0.5rem;"></span>
                <span class="visually-hidden">Next</span>
              </div>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Form starts here -->
    <form @submit.prevent="submitForm">
      <!-- User information display -->
      <div class="mb-3 user-info">
        <div class="d-flex justify-content-between">
          <h3>Anna Maria Tamm Rodriguez Espinosa</h3>
          <button type="button" class="btn btn-link">Edit</button>
        </div>
        <p class="text-muted">
          38912052254 / +372 5289 6572 / anna.tamm@gmail.com
        </p>
      </div>

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
import { ref } from 'vue'

defineProps({
  msg: String,
})

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

