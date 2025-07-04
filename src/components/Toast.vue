<script setup>
import { useToast } from '@/composables/useToast.js';
import { TransitionRoot } from '@headlessui/vue';
import { computed } from 'vue';

const { toast } = useToast();

const bgColor = computed(() => {
    switch (toast.value.type) {
        case 'success':
            return 'bg-green-500';
        case 'error':
            return 'bg-red-500';
        case 'warning':
            return 'bg-yellow-500';
        case 'info':
            return 'bg-blue-500';
        default:
            return 'bg-gray-500';
    }
});
</script>

<template>
    <TransitionRoot
        appear
        :show="toast.show"
        enter="transform ease-out duration-300 transition"
        enter-from="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2"
        enter-to="translate-y-0 opacity-100 sm:translate-x-0"
        leave="transition ease-in duration-100"
        leave-from="opacity-100"
        leave-to="opacity-0"
    >
        <div
            v-show="toast.show"
            class="fixed bottom-4 right-4 z-50"
        >
            <div :class="[bgColor, 'rounded-lg shadow-lg overflow-hidden max-w-xl']">
                <div class="p-4">
                    <div class="flex items-start">
                        <div class="ml-3 w-0 flex-1 pt-0.5">
                            <p class="text-sm font-medium text-white">
                                {{ toast.message }}
                            </p>
                        </div>
                        <div class="ml-4 flex-shrink-0 flex">
                            <button
                                type="button"
                                class="rounded-md inline-flex text-white hover:text-gray-200 focus:outline-none"
                                @click="toast.show = false"
                            >
                                <span class="sr-only">Close</span>
                                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </TransitionRoot>
</template> 