<script setup>
import { computed } from 'vue'

const props = defineProps({
  variant: {
    type: String,
    default: 'default',
    validator: (value) => {
      return ['default', 'secondary', 'destructive', 'outline'].includes(value)
    }
  }
})

const classes = computed(() => {
  return {
    'inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2': true,
    'border-transparent bg-primary text-primary-foreground hover:bg-primary/80': props.variant === 'default',
    'border-transparent bg-secondary text-secondary-foreground hover:bg-secondary/80': props.variant === 'secondary',
    'border-transparent bg-destructive text-destructive-foreground hover:bg-destructive/80': props.variant === 'destructive',
    'text-foreground': props.variant === 'outline'
  }
})
</script>

<template>
  <div :class="classes">
    <slot />
  </div>
</template>