<template>
  <div class="loan-form">
    <!-- Carusel for the loan -->
    <div id="carousel1" class="carousel slide" data-bs-touch="false">
      <div class="bg-primary text-textWhite rounded-pill py-2 gx-2 d-flex" >
        <div class="carousel-inner overflow-visible">
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
                <div class="fw-light lh-base fs-6 row text-end">
                  
                  <div class="col-6 px-0">Amount</div>
                  <!-- Example split danger button -->
                  <div class="btn-group col">
                    <input type="text" v-model="selectedAmount" id="amount" class="form-control bg-transparent border-0 border-bottom text-textWhite p-0 rounded-0" style="width: 60px;">
                    <div class="dropdown-toggle-split" data-bs-toggle="dropdown" aria-expanded="false"><i class="bi-chevron-down"></i></div>
                    <ul class="dropdown-menu px-2" style="overflow: scroll;height: 166px;">
                      <li v-for="(amount, index) in amounts" :key="index" @click="submitValue(amount.value)">
                        <div v-if="amount.ismin || amount.ismax" class="dropdown-item d-flex justify-content-between">
                          <div class="col d-flex align-items-start">
                            {{amount.value}}<span style="font-size: 10px;padding-bottom: 1rem;">€</span>
                          </div>
                          <div v-if="amount.ismin" class="col" style="font-size: 10px;">
                            Min. allowed
                          </div>
                          <div v-if="amount.ismax" class="col" style="font-size: 10px;">
                            Max. allowed
                          </div>
                        </div>
                        <div v-else class="dropdown-item d-flex justify-content-center">
                          <div class="col d-flex align-items-start">
                            {{amount.value}}<span style="font-size: 10px;padding-bottom: 1rem;">€</span>
                          </div>
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
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
          <button type="button" class="btn btn-link"><i class="bi bi-pen-fill"></i></button>
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
document.activeElement.blur();
const selectedAmount = ref('')
const submitValue = (value) => {
  selectedAmount.value = value
}

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
// thank you chatGPT )))
const amounts = [
  { value: 200, ismin: true, ismax: false },
  { value: 250, ismin: false, ismax: false },
  { value: 300, ismin: false, ismax: false },
  { value: 350, ismin: false, ismax: false },
  { value: 400, ismin: false, ismax: false },
  { value: 450, ismin: false, ismax: false },
  { value: 500, ismin: false, ismax: false },
  { value: 550, ismin: false, ismax: false },
  { value: 600, ismin: false, ismax: false },
  { value: 650, ismin: false, ismax: false },
  { value: 700, ismin: false, ismax: false },
  { value: 750, ismin: false, ismax: false },
  { value: 800, ismin: false, ismax: false },
  { value: 850, ismin: false, ismax: false },
  { value: 900, ismin: false, ismax: false },
  { value: 950, ismin: false, ismax: false },
  { value: 1000, ismin: false, ismax: false },
  { value: 1100, ismin: false, ismax: false },
  { value: 1200, ismin: false, ismax: false },
  { value: 1300, ismin: false, ismax: false },
  { value: 1400, ismin: false, ismax: false },
  { value: 1500, ismin: false, ismax: false },
  { value: 2000, ismin: false, ismax: false },
  { value: 2500, ismin: false, ismax: false },
  { value: 3000, ismin: false, ismax: false },
  { value: 3500, ismin: false, ismax: false },
  { value: 4000, ismin: false, ismax: false },
  { value: 4500, ismin: false, ismax: false },
  { value: 5000, ismin: false, ismax: false },
  { value: 5500, ismin: false, ismax: false },
  { value: 6000, ismin: false, ismax: false },
  { value: 6500, ismin: false, ismax: false },
  { value: 7000, ismin: false, ismax: false },
  { value: 7500, ismin: false, ismax: false },
  { value: 8000, ismin: false, ismax: false },
  { value: 8500, ismin: false, ismax: false },
  { value: 9000, ismin: false, ismax: false },
  { value: 9500, ismin: false, ismax: false },
  { value: 10000, ismin: false, ismax: true }
];
</script>

<style scoped>
.loan-form {
  max-width: 764px;
}
li:first-child {
  border-bottom: 1px solid #413C3C;
}
li:last-child {
  border-bottom: 1px solid #413C3C;
}
</style>

