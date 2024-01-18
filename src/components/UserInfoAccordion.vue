<template>
  <div class="mb-4" id="accordionExample">
    <div class="">
      <div v-if="formEdit" class="py-3 d-flex justify-content-between align-items-center w-100 bg-info rounded-pill border-4 border-info">
        <div class="col-4 fs-6 d-flex justify-content-center" >
          <label class="fs-6">
            Change your contact Info
          </label>
        </div>
        <div class="col-2 p-0 m-0 d-flex align-items-center">
          <div class="col-1 border-bottom border-grey p-0" style="height: 25px;">+</div>
          <input type="phone" v-model.number="userData.phone" id="phone" class="col-5 form-control bg-transparent border-0 border-bottom border-grey p-0 rounded-0">
        </div>
        <div class="col-3 p-0">
          <input type="email" v-model.number="userData.email" id="email" class="col form-control bg-transparent border-0 border-bottom border-grey p-0 rounded-0">
        </div>
        <div class="col-1 ">
          <button class="bg-primary rounded-circle border-0" style="width: 31px;height: 31px;" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne" @click="editForm()"><i class="bi-chevron-right text-textWhite"></i></button>
        </div>
      </div>
      <div v-else="!formEdit" class="border border-4 border-light" style="border-radius: 35px">
        <div class="py-3 d-flex justify-content-between align-items-center bg-info" style="border-radius: 30px 30px 0px 0px;">
          <div class="col-6 offset-3" style="font-size: 18px;">Anna Maria Tamm Rodriguez Espinosa</div>
          <div class="col-1 ">
            <button class="bg-textWhite rounded-circle border-0 " style="width: 31px;height: 31px;" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne" @click="editForm()"><i class="bi bi-pen-fill"></i></button>
          </div>
        </div>
        <div id="collapseOne" class="py-2 accordion-collapse collapse show" data-bs-parent="#accordionExample">
          <div class="row m-0 text-center ">
            <div class="col">
              <i class="bi bi-person-bounding-box mx-1"></i>{{userData.id_code}}
            </div>
            <div class="col">
              <i class="bi bi-telephone mx-1"></i>+{{userData.phone}}
            </div>
            <div class="col">
              <i class="bi bi-envelope mx-1"></i>{{userData.email}}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const formEdit = ref(false)

const userData = ref({
  id_code: 38912052254,
  phone: 37252896572,
  email: 'anna.tamm@gmail.com'
})

const editForm = () => {
  formEdit.value = !formEdit.value
}

</script>
<style scoped>
input:hover {
  border-bottom: #2B0A57;
}
</style>