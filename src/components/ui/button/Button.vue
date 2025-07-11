<script setup>
import { computed } from 'vue'
import { useRouter } from 'vue-router'
import { cn } from '@/lib/utils'

const props = defineProps({
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'destructive', 'outline', 'secondary', 'ghost', 'link'].includes(value),
  },
  size: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'sm', 'lg', 'icon'].includes(value),
  },
  className: {
    type: String,
    default: '',
  },
  href: {
    type: String,
    default: undefined
  }
});

const router = useRouter();

const baseStyles = 'inline-flex items-center justify-center rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50'

const variants = {
  default: 'bg-primary text-primary-foreground hover:bg-primary/90',
  destructive: 'bg-destructive text-destructive-foreground hover:bg-destructive/90',
  outline: 'border border-input bg-background hover:bg-accent hover:text-accent-foreground',
  secondary: 'bg-secondary text-secondary-foreground hover:bg-secondary/80',
  ghost: 'hover:bg-accent hover:text-accent-foreground',
  link: 'text-primary underline-offset-4 hover:underline'
}

const sizes = {
  default: 'h-10 px-4 py-2',
  sm: 'h-9 rounded-md px-3',
  lg: 'h-11 rounded-md px-8',
  icon: 'h-10 w-10'
}

const classes = computed(() => {
  return cn(
    baseStyles,
    variants[props.variant],
    sizes[props.size],
    props.className
  )
})

const handleClick = (e) => {
  if (props.href) {
    e.preventDefault()
    if (props.href.startsWith('http')) {
      // External link
      window.open(props.href, '_blank')
    } else {
      // Internal navigation
      router.push(props.href)
    }
  }
}
</script>

<template>
  <button 
    :class="classes" 
    v-bind="$attrs"
    @click="handleClick"
  >
    <slot />
  </button>
</template> 