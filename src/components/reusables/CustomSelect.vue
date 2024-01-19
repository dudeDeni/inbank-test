<template>
  <div class="position-relative">
    <div :class="selectLabelClass" class="fs-6">{{label}}</div>
    <select :id="id" :autocomplete="id" class="form-select" @input="update($event.target.value)" :placeholder="label" :value="modelValue" >
      <option v-for="(item, index) in items" :key="index" :value="item">{{item}}</option>
    </select>
  </div>
</template>
<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  label: {
    type: [String, Boolean],
    default: '',
  },
  items: {
    type: Array,
    default: () => [],
  },
  id: {
    type: String,
    default: '',
  },
  ariaLabel: {
    type: String,
    default: '',
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  modelValue: {
    type: [String, null],
    default: '',
  }
})

const emit = defineEmits(['update'])
const isActive = ref(props.modelValue ? true : false)

const update = (value) => {
  isActive.value = true
  emit('update', value)
}

const selectLabelClass = computed(() => ({
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