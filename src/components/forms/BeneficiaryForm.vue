<template>
  <div>
    <div class="row text-center mb-3">
      <div class="col-6 offset-3 mb-3 form-check d-flex align-items-center">
        <input type="checkbox" class="form-check-input" id="pepCheck" v-model="isMemberPep">
        <label class="form-check-label mx-2" for="pepCheck">Neither I nor my family member is PEP</label>
      </div>
      <div class="col-2">
        <div type="button" data-bs-toggle="modal" data-bs-target="#modal1">
          <i class="bi bi-info-circle"></i>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="modal1" tabindex="-1" aria-labelledby="modal1" aria-hidden="true">
          <div class="modal-dialog modal-md">
            <div class="modal-content">
              <div class="d-flex justify-content-start">
                <div type="button" class="btn-close mt-2 mx-2" data-bs-dismiss="modal" aria-label="Close"></div>
              </div>
              <div class="modal-body text-start" style="margin-block: 10rem;">
                <h1>PEP</h1>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="!isMemberPep">
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomSelect :label="'Relationship to the PEP'" :id="'member_relationship'" :model-value="formData.memberRelationship" @update="updateField($event, 'memberRelationship')"/>
        </div>
        <div class="col">
          <CustomSelect :label="'PEP region'" :id="'member_region'" :model-value="formData.memberRegion" @update="updateField($event, 'memberRegion')"/>
        </div>
      </div>
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomSelect :label="'PEP position'" :id="'member_position'" :model-value="formData.memberPosition" @update="updateField($event, 'memberPosition')"/>
        </div>
        <div class="col">
          <CustomSelect :label="'Duration as PEP or related to a PEP'" :id="'member_duration'" :model-value="formData.memberDuration" @update="updateField($event, 'memberDuration')"/>
        </div>
      </div>
    </div>
    <!-- =============== -->
    <div class="row text-center mb-3 mt-3">
      <div class="col-6 offset-3 mb-3 form-check d-flex align-items-center">
        <input type="checkbox" class="form-check-input" id="beneficiaryCheck" v-model="isUltimate">
        <label class="form-check-label mx-2" for="beneficiaryCheck">I'm the ultimate beneficiary beneficiary</label>
      </div>
      <div class="col-2">
        <div type="button"  data-bs-toggle="modal" data-bs-target="#modal2">
          <i class="bi bi-info-circle"></i>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="modal2" tabindex="-1" aria-labelledby="modal2" aria-hidden="true">
          <div class="modal-dialog modal-md">
            <div class="modal-content">
              <div class="d-flex justify-content-start">
                <div type="button" class="btn-close mt-2 mx-3" data-bs-dismiss="modal" aria-label="Close"></div>
              </div>
              <div class="modal-body text-start" style="margin-block: 10rem;">
                <h1>PEP</h1>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="!isUltimate">
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomInput :label="'First name'" :type="'name'" :id="'firstName'" :model-value="formData.firstName" @update="updateField($event, 'firstName')"/>
        </div>
        <div class="col">
          <CustomInput :label="'Last name'" :type="'name'" :id="'lastName'" :model-value="formData.lastName" @update="updateField($event, 'lastName')"/>
        </div>
      </div>
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomInput :label="'Personal ID code'" :type="'text'" :id="'personalCode'" :model-value="formData.personalCode" @update="updateField($event, 'personalCode')"/>
        </div>
        <div class="col">
          <CustomSelect :label="'Residency'" :id="'residency'" :model-value="formData.residency" @update="updateField($event, 'residency')"/>
        </div>
      </div>
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomInput :label="'Birth place'" :type="'text'" :id="'birthPlace'" :model-value="formData.birthPlace" @update="updateField($event, 'birthPlace')"/>
        </div>
        <div class="col">
          <CustomInput :label="'Birth date'" :type="'text'" :id="'birthDate'" :model-value="formData.birthDate" @update="updateField($event, 'birthDate')"/>
        </div>
      </div>
    </div>
    <!-- ============== -->
    <div class="row text-center mb-3 mt-3">
      <div class="col-6 offset-3 mb-3 form-check d-flex align-items-center">
        <input type="checkbox" class="form-check-input" id="isOwnerPep" v-model="isOwnerPep">
        <label class="form-check-label mx-2" for="isOwnerPep">The beneficial owner is not a PEP</label>
      </div>
    </div>
    <div v-if="!isOwnerPep">
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomSelect :label="'Relationship to the PEP'" :id="'owner_relationship'" :model-value="formData.ownerRelationship" @update="updateField($event, 'ownerRelationship')"/>
        </div>
        <div class="col">
          <CustomSelect :label="'PEP region'" :id="'owner_region'" :model-value="formData.ownerRegion" @update="updateField($event, 'ownerRegion')"/>
        </div>
      </div>
      <div class="row g-3 mb-3">
        <div class="col">
          <CustomSelect :label="'PEP position'" :id="'owner_position'" :model-value="formData.ownerPosition" @update="updateField($event, 'ownerPosition')"/>
        </div>
        <div class="col">
          <CustomSelect :label="'Duration as PEP or related to a PEP'" :id="'owner_duration'" :model-value="formData.ownerDuration" @update="updateField($event, 'ownerDuration')"/>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import CustomSelect from '../reusables/CustomSelect.vue';
import CustomInput from '../reusables/CustomInput.vue';
import { ref } from 'vue'

const isMemberPep = ref(false);
const isUltimate = ref(false);
const isOwnerPep = ref(false);

const formData = ref({
  memberRelationship: null,
  memberRegion: null,
  memberPosition: null,
  memberDuration: null,
  firstName: null,
  lastName: null,
  personalCode: null,
  residency: null,
  birthPlace: null,
  birthDate: null,
  ownerRelationship: null,
  ownerRegion: null,
  ownerPosition: null,
  ownerDuration: null,
})
</script>