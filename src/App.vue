<script setup>
import { reactive, computed } from 'vue'
import ItemSelect from './components/ItemSelect.vue'
import ComparisonSummary from './components/ComparisonSummary.vue'

const data = reactive({
  list: [],
  compareItemIdFirst: null,
  compareItemIdSecond: null
})

const compareItems = computed(() => {
  const firstItem = data.list.find(item => item.id === +data.compareItemIdFirst)
  const secondItem = data.list.find(item => item.id === +data.compareItemIdSecond)

  return [firstItem, secondItem].sort((a, b) => a.price - b.price)
})

const fetchItemList = async () => {
  try {
    const res = await fetch('https://dummyjson.com/products')
    const { products } = await res.json()
    data.list = products
  } catch (error) {
    console.debug(error)
  }
}

fetchItemList()

</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Select items to compare</h1>
    <div class="flex flex-col gap-5 justify-center">
      <ItemSelect
        :list="data.list"
        v-model:selectedId="data.compareItemIdFirst"
      />
      <ItemSelect
        :list="data.list"
        v-model:selectedId="data.compareItemIdSecond"
      />
    </div>
    <ComparisonSummary
      v-if="compareItems[0] && compareItems[1]"
      :items="compareItems"
    />
  </div>
</template>
