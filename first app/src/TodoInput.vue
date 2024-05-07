<script setup>
import { ref } from 'vue';
const emit = defineEmits(['create']);
var newTask = ref('');
function createTask() {
    const text = newTask.value;
    console.log(text);
    if(text === "") {
        document.getElementById('error').innerText = "Nie możesz dodać pustego zadania!";
    } else {
        emit('create', text);
        document.getElementById('error').innerText = "";
    }
}
</script>

<template>
    <label for="">Dodaj zadanie: </label>
    <input type="text" v-model="newTask" v-on:keyup.enter="createTask()">
    <button @click="createTask()">Dodaj</button>
    <p id="error"></p>
</template>