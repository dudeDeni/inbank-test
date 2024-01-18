<template>
  <div class="position-relative">
    <div :class="labelClass">
      <label class="fs-6"> {{ label }}</label>
    </div>
    <input 
      :type="type" 
      :id="id" 
      :value="modelValue" 
      @input="$emit('update:modelValue', $event.target.value)"
      v-bind="$attrs"
      class="form-control"
      @focus="toggle('focus')"
      @blur="toggle('blur')"
    />
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
const props = defineProps({
  label: {
    type: String,
    default: '',
  },
  type: {
    type: String,
    default: '',
  },
  id: {
    type: String,
    default: '',
  },
  modelValue: {
    type: String,
    default: '',
  }
})

const isActive = ref(false)

const toggle = (event) => {
  if (event == 'focus') {
    isActive.value = true
  }
  else {
    isActive.value = false
  }
}

const labelClass = computed(() => ({
  'position-absolute bg-textWhite': true,
  'px-1': true,
  'up': isActive.value,
  'down': !isActive.value
}))
</script>

<style scoped>
.up {
  top: -0.9rem;
  left: 1rem;
  transition: all 0.2s ease-out;
}

.down {
  top: 6px;
  left: 0.5rem;
  transition: all 0.2s ease-out;
}
</style>