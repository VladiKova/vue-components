<script setup>
defineProps({
    start: Number,
    end: Number,
    length: Number
});
const emit = defineEmits(['next', 'previous']);


</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-outline-primary" @click="emit('previous')"
            :disabled="start <= 0">Previous</button>
        <button type="button" class="btn btn-outline-primary" @click="emit('next')" :disabled="end >= length">Next</button>
    </div>
</template>