<script setup>
import { defineProps, defineEmits } from 'vue'
import { useItemComparison } from '../composables/itemComparison'

const props = defineProps({
  list: {
    type: Array,
    default: () => ([])
  },
  selectedId: {
    type: Number,
    default: null
  }
})

const emit = defineEmits(['update:selectedId'])
</script>

<template>
  <select
    :value="selectedId"
    @input="$emit('update:selectedId', +$event.target.value)"
    class="p-2 border-2 border-gray-dark"
  >
    <option disabled value="">Select an item</option>
    <option v-for="item in props.list" :key="item.id" :value="item.id">
      {{ `${item.title} - $${item.price}` }}
    </option>
  </select>
</template>
