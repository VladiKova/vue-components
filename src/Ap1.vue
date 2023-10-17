<script setup>
import { ref, computed } from 'vue';
const counter = ref(0);
const buttonDesc = ref(['Up', 'Down', 'Reset', 'Add']);
const favNumbers = ref([]);
const modifyCounter = (action) => {
    switch (action) {
        case 'up': counter.value++;
            break;
        case 'down': counter.value--;
            break;
        case 'reset': counter.value = 0;
            break;

    }
}
const addNumber = () =>  favNumbers.value = [...favNumbers.value, counter.value];;


const className = computed(() => {
    if (counter.value == 0) {
        return 'color3';
    } else if (counter.value > 0) {
        return 'color1';
    } else {
        return 'color2';
    }
});
</script>
<template>
    <div class="container text-center">

        <h1>Contador</h1>
        <h2 :class="className">{{ counter }}</h2>
        <ul class="list-group">
            <li v-for="(number,index) in favNumbers" :key="index" class="list-group-item text-primary bg-dark">
                {{ number }}
            </li>
        </ul>
        
        <div>
            <button @click="modifyCounter('up')" class="btn btn-success">
                {{ buttonDesc[0] }}
            </button>
            <button @click="modifyCounter('down')" class="btn btn-danger">
                {{ buttonDesc[1] }}
            </button>
            <button @click="modifyCounter('reset')" class="btn btn-warning">
                {{ buttonDesc[2] }}
        </button>
        <button @click="addNumber" :disabled="favNumbers.includes(counter)" class="btn btn-info">
            {{ buttonDesc[3] }}
        </button>
    </div>
</div>
</template>
<style>
.color1 {
    color: rgb(0, 255, 0);
}

.color2 {
    color: red;
}

.color3 {
    color: blue;
}

div {
    display: block;
}

button {
    margin: 1px;
}
</style>