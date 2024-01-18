<template>
  <div class="mb-3">
    <label for="country" class="form-label">Country</label>
    <select id="country" class="form-select" v-model="props.country">
      <option selected>World</option>
      <!-- Populate with actual country options -->
    </select>
  </div>

  <div class="row g-3 mb-3">
    <div class="col-md">
      <label for="city" class="form-label">City / Parish</label>
      <input type="text" id="city" class="form-control" v-model="props.city">
    </div>
    <div class="col-md">
      <label for="county" class="form-label">County</label>
      <input type="text" id="county" class="form-control" v-model="props.county">
    </div>
  </div>

  <div class="row g-3 mb-3">
    <div class="col-md">
      <label for="street" class="form-label">Street</label>
      <input type="text" id="street" class="form-control" v-model="props.street">
    </div>

    <div class="col-md-4">
      <label for="house" class="form-label">House</label>
      <input type="text" id="house" class="form-control" v-model="props.house">
    </div>

    <div class="col-md-4">
      <label for="apartment" class="form-label">Apartment</label>
      <input type="text" id="apartment" class="form-control" v-model="props.apartment">
    </div>
    <div class="col-md-4">
      <label for="postalCode" class="form-label">Postal Code</label>
      <input type="text" id="postalCode" class="form-control" v-model="props.postalCode">
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  country: String,
  city: String,
  county: String,
  street: String,
  house: String,
  apartment: String,
  postalCode: String,
})
</script>