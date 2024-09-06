<script setup lang="ts">
const props = defineProps({
  customerTypes: String
})

let customerType: Ref<string | null> = ref(null)

const expandedCustomerTypes = computed(() => {
  if(props.customerTypes) {
    return props.customerTypes.split(',')
  }
})

const conditionMet = computed(() => {
  if(expandedCustomerTypes.value && customerType.value) {
    return expandedCustomerTypes.value.includes(customerType.value)
  }
})

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search)
  customerType.value = urlParams.get('customerType')
})
</script>

<template>
  <template v-if="conditionMet">
    <slot/>
  </template>
</template>