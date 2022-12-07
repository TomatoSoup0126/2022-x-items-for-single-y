<script setup>
import { defineProps, computed } from 'vue'

const props = defineProps({
  items: {
    type: Array,
    default: () => ([])
  }
})

const multiple = computed(() => props.items[1].price / props.items[0].price)
</script>

<template>
  <p class="mx-5 text-center" v-if="(items[0].id !== items[1].id)">
    You can get
    <strong>{{ `${Math.round(multiple)}x ` }}</strong>
    <em>{{ items[0].title }}</em>
    for about the same price as a single
    <em>{{ items[1].title }}</em>
  </p>
  <p v-else>
    These are the same items
  </p>
</template>
