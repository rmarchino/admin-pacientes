
<script setup>
import { computed } from 'vue';

const props = defineProps({
    alerta: {
        type: Object,
        required: true
    }
})

const isError = computed(() => {
    return props.alerta.type === 'error'
})

</script>

<template>
    <div 
        :class="[isError ? 'bg-red-500' : 'bg-green-500']"
        class=" p-3 mb-3 text-white  uppercase text-center rounded-lg"
    >
        {{ alerta.message }}
    </div>
</template>