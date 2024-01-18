<template>
  <div class="d-flex justify-content-center border-top border-bottom border-greyLight position-relative text-center my-5">
    <div class="d-flex text-center justify-content-center position-absolute top-0 start-50 translate-middle bg-textWhite text-greyLight" style="width: 30%;">Or</div>
    <div class="my-4 form-check form-switch d-flex">
      <input class="form-check-input d-flex" type="checkbox" role="switch" id="flexSwitchCheckDefault" @input="checkboxToggle($event)">
      <label class="form-check-label d-flex mx-3" for="flexSwitchCheckDefault">Add address manually</label>
    </div>
  </div>
</template>
<script setup>
const emit = defineEmits(['checkManually'])

function checkboxToggle(event) {
  emit('checkManually', event.target.checked)
}
</script>