<template>
  <div>
    <div class="row g-3 mb-3">
      <div class="col">
        <CustomInput :disabled="true" :label="'Country'" :type="'text'" :id="'country'" :model-value="fields.country" @update="updateField($event, 'country')"/>
      </div>
      <div class="col">
        <CustomSelect :label="'County'" :id="'county'" :items="props.counties" :model-value="fields.county" @update="updateField($event, 'county')"/>
      </div>
    </div>
    <div class="row g-3 mb-3">
      <div class="col">
        <CustomSelect :label="'City/Parish'" :id="'address-level1'" :items="props.cities" :model-value="fields.city" @update="updateField($event, 'city')"/>
      </div>
      <div class="col">
        <CustomSelect :label="'Township/Village'" :id="'town'" :items="props.towns" :model-value="fields.townShip" @update="updateField($event, 'town')"/>
      </div>
    </div>
    <div class="row g-3 mb-3">
      <div class="col">
        <CustomInput :label="'Street'" :type="'address-line1'" :id="'address-line1'" :model-value="fields.street" @update="updateField($event, 'street')"/>
      </div>
      <div class="col">
        <div class="row">
          <div class="col">
            <CustomInput :label="'House'" :type="'house'" :id="'house'" :model-value="fields.house" @update="updateField($event, 'house')"/>
          </div>
          <div class="col">
            <CustomInput :label="'Apartment'" :type="'apartment'" :id="'apartment'" :model-value="fields.apartment" @update="updateField($event, 'apartment')"/>
          </div>
          <div class="col">
            <CustomInput :label="'Postal Code'" :type="'postal_code'" :id="'postal_code'" :model-value="fields.postalCode" @update="updateField($event, 'postalCode')"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import CustomSelect from '../reusables/CustomSelect.vue';
import CustomInput from '../reusables/CustomInput.vue';
import { ref } from 'vue'

const emit = defineEmits(['update'])

const props = defineProps({
  country: String,
  city: String,
  county: String,
  street: String,
  house: String,
  apartment: String,
  postalCode: String,
  cities: Array,
  counties: Array,
  towns: Array
})
const fields = ref({
  country: props.country,
  city: props.city,
  county: props.county,
  townShip: props.townShip,
  street: props.street,
  house: props.house,
  apartment: props.apartment,
  postalCode: props.postalCode
})

const updateField = (event, targetField) => {
  console.log(typeof(event), targetField)
  fields.value[targetField] = event
  const payload = {
    target: targetField,
    value: event
  }

  emit('update', payload)
}
</script>