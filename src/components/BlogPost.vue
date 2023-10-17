<script setup>

defineProps({
    id: Number,
    title: String,
    body: {
        type: String,
        default: 'Not description'
    }
});
const emit = defineEmits(['changeFav']);
</script>
<template>
    <div class="card bg-dark">
        <div class="card-body">
            <h4 class="card-title">Post ID: {{ id }} - {{ title }}</h4>
            <p><b>Description</b> {{ body }}</p>
            <button class="btn btn-warning align-self-center" @click="emit('changeFav',title)">Select as favorite</button>
        </div>
    </div>
</template>
                  
<style></style>