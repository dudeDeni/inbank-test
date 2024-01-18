<template>
  <div class="row g-3 mb-3">
    <div class="col">
      <CustomInput :label="'Country'" :type="'text'" :id="'country'"/>
    </div>
    <div class="col">
      <CustomInput :label="'County'" :type="'text'" :id="'county'"/>
    </div>
  </div>
  <div class="row g-3 mb-3">
    <div class="col">
      <CustomInput :label="'City/Parish'" :type="'text'" :id="'city'"/>
    </div>
    <div class="col">
      <CustomInput :label="'Township/Village'" :type="'text'" :id="'town'"/>
    </div>
  </div>
  <div class="row g-3 mb-3">
    <div class="col">
      <CustomInput :label="'Street'" :type="'text'" :id="'street'"/>
    </div>
    <div class="col">
      <div class="row">
        <div class="col">
          <CustomInput :label="'House'" :type="'text'" :id="'house'"/>
        </div>
        <div class="col">
          <CustomInput :label="'Apartment'" :type="'text'" :id="'apartment'"/>
        </div>
        <div class="col">
          <CustomInput :label="'Postal Code'" :type="'text'" :id="'postal code'"/>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import CustomInput from '../reusables/CustomInput.vue'

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