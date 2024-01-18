<template>
  <!-- Carusel for the loan -->
  <div ref="carousel" id="carousel1" class="carousel slide carousel-fade mb-4" data-bs-touch="false">
    <div class="bg-primary text-textWhite rounded-pill py-2 gx-2 d-flex" >
      <div class="carousel-inner overflow-visible" >
        <div ref="slide1" class="carousel-item active">
          <button class="carousel-control-prev" type="button" data-bs-target="#carousel1" data-bs-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true" style="height: 13px;"></span>
          </button>
          <div class="row align-items-center m-0 px-0">
            <div class="col-6 d-flex justify-content-end">
              <div class="fw-light lh-lg fs-5">Your loan application</div>
            </div>
            <div class="col">
              <div class="fw-lighter d-flex">{{selectedAmount}}<span class="" style="font-size: 14px;">€</span>&nbsp;/<span class="fw-lighter">&nbsp;{{selectedMonths}}&nbsp;months</span></div>
            </div>
          </div>
        </div>

        <div ref="slide2" class="carousel-item" style="height: 40px;" >
          <div class="row align-items-center text-left m-0 px-0" style="height: 40px;">
            <div class="col-4 p-0">
              <div class="fw-light lh-base fs-6 row text-end">
                <div class="col-5 px-0 position-relative">
                  <div class="fw-light lh-base fs-6 d-flex align-items-center justify-content-end">Amount</div>
                  <span v-show="hasError" class="text-danger position-absolute w-100 bottom-20 start-0" style="font-size: 10px;">Out of range</span>
                  <span v-show="rangeAmount" class="text-textWhite position-absolute w-100 bottom-20 start-0" style="font-size: 10px;">200 - 10 000 €</span>
                </div>
                <!-- Example split danger button -->
                <div class="btn-group col-6 offset-1">
                  <div class="row p-0">
                    <input type="text" v-model="selectedAmount" id="amount" class="col form-control bg-transparent border-0 border-bottom border-textWhite text-textWhite p-0 rounded-0" style="width: 47px;height: 25px;">
                    <div class="col border-bottom border-textWhite p-0" style="height: 25px;">€</div>
                  </div>
                  <div class="dropdown-toggle-split mx-2 d-flex align-items-center" data-bs-toggle="dropdown" aria-expanded="false"><i class="bi-chevron-down"></i></div>
                  <ul class="dropdown-menu px-2" style="overflow: scroll;height: 166px;">
                    <li v-for="(amount, index) in amounts" :key="index" @click="submitValue(amount.value, 'amount')">
                      <div v-if="amount.ismin || amount.ismax" class="dropdown-item d-flex justify-content-between">
                        <div class="col d-flex align-items-start">
                          {{amount.value}}<span style="font-size: 10px;">€</span>
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
                          {{amount.value}}<span style="font-size: 10px;">€</span>
                        </div>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="col-3 p-0">
              <div class="fw-light lh-base fs-6 row text-end">
                <label for="duration" class="col-5 fw-light lh-base fs-6 d-flex align-items-center">Duration</label>
                <div class="btn-group col-6 offset-1 p-0">
                  <div class="row p-0">
                    <input type="text" v-model="selectedMonths" id="duration" class="col form-control bg-transparent border-0 border-bottom border-textWhite text-textWhite p-0 rounded-0" style="width: 20px;">
                    <div class="col border-bottom border-textWhite p-0">months</div>
                  </div>
                  <div class="mx-2 dropdown-toggle-split" data-bs-toggle="dropdown" aria-expanded="false"><i class="bi-chevron-down"></i></div>
                  <ul class="dropdown-menu px-2" >
                    <li v-for="(month, index) in months" :key="index" @click="submitValue(month, 'month')">
                      <div class="dropdown-item d-flex justify-content-center">
                        <div class="">
                          {{month}}
                        </div>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="col-4 p-0">
              <div class="row p-0 m-0 bg-secondary rounded-pill ">
                <div class="col-6 offset-1 p-0 fw-light lh-base fs-6 d-flex justify-content-center align-items-center">Monthly Payment</div>
                <div class="col offset-1 p-0 d-flex align-items-center fs-5">{{ monthlyPayment }}<span style="font-size: 14px;">€</span></div>
              </div>
            </div>
          </div>
          
          <button :disabled="!selectedAmount || rangeAmount || hasError" class="col carousel-control-next" type="button" data-bs-target="#carousel1" data-bs-slide="next" @mouseover="checkAmount()">
            <div class="bg-white rounded-pill" style="height: 2rem;">
              <span class="carousel-control-next-icon" aria-hidden="true" style="height: 15px;margin-top: 0.5rem;"></span>
              <span class="visually-hidden">Next</span>
            </div>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, watch } from 'vue'

const selectedAmount = ref(200)
const selectedMonths = ref(36)
const monthlyPayment = ref((selectedAmount.value/selectedMonths.value).toFixed(2))
const hasError = ref(false)
const rangeAmount = ref(false)

const submitValue = (value, field) => {
  if (field === 'amount') {
    selectedAmount.value = value
  } else if (field === 'month') {
    selectedMonths.value = value
  }
}

const checkAmount = () => {
  if (!selectedAmount.value) {
    rangeAmount.value = false
    hasError.value = true
  }
  if (selectedAmount.value < amounts[0].value) {
    rangeAmount.value = false
    hasError.value = true
  }
  
}

watch([selectedAmount, selectedMonths], (newValues, prevValues) => {
  monthlyPayment.value = (selectedAmount.value/selectedMonths.value).toFixed(2)
  hasError.value = false
  if (selectedAmount.value < amounts[0].value) {
    rangeAmount.value = true
  }
})
const months = [12,24,36,48]
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
li:first-child {
  border-bottom: 1px solid #413C3C;
}
li:last-child {
  border-bottom: 1px solid #413C3C;
}
</style>