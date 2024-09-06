<script setup lang="ts">
const props = defineProps({
  customerTypes: String
})

let customerType: string | null = null

const expandedCustomerTypes = computed(() => {
  if(props.customerTypes) {
    return props.customerTypes.split(',')
  }
})

const conditionMet = computed(() => {
  if(expandedCustomerTypes.value && customerType) {
    return expandedCustomerTypes.value.includes(customerType)
  }
})

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search)
  customerType = urlParams.get('customerType')
})
</script>
<template>
  <template>
    <slot/>
  </template>
</template>