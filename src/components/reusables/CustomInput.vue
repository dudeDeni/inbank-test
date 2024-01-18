<template>
  <div class="position-relative w-100">
    <div v-if="label" :class="labelClass">
      <label :for="id" class="fs-6"> {{ label }}</label>
    </div>
    <input 
      :type="type" 
      :id="id" 
      :value="modelValue" 
      @input="update($event.target.value)"
      v-bind="$attrs"
      class="form-control"
      @focus="toggle('focus')"
      @blur="toggle('blur')"
      :autocomplete="type"
    />
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  label: {
    type: [String, Boolean],
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
    type: [String, null],
    default: '',
  }
})

const emit = defineEmits(['update'])

const isActive = ref(props.modelValue ? true : false)

const update = (value) => {
  emit('update', value)
}

const toggle = (event) => {
  if (event == 'focus') {
    isActive.value = true
  }
  else {
    if (!props.modelValue) {
      isActive.value = false
    }
  }
}

const labelClass = computed(() => ({
  'position-absolute bg-textWhite rounded-3': true,
  'px-1': true,
  'up': isActive.value,
  'down': !isActive.value
}))
</script>

<style scoped>
.up {
  top: -0.9rem;
  left: 0.5rem;
  transition: all 0.2s ease-out;
}

.down {
  top: 6px;
  left: 0.5rem;
  transition: all 0.2s ease-out;
}
</style>