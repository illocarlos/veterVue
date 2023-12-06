<script setup>
import { defineProps, computed } from "vue";

const props = defineProps({
    alert: {
        type: Object,
        required: true
    }
});

const isError = computed(() => {

    return props.alert.type === 'error';
});
</script>

<template>
    <div :class="[isError ? 'bg-red-500' : 'bg-green-500']" 
    class="text-white font-bold uppercase text-center rounded-lg">
        {{ alert.message }}
    </div>
</template>

