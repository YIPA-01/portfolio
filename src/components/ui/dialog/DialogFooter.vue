<script setup>
const props = defineProps({
  class: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div 
    :class="[
      'flex flex-col-reverse sm:flex-row sm:justify-end sm:space-x-2',
      props.class
    ]"
  >
    <slot />
  </div>
</template> 