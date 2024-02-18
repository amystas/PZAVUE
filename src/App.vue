<script setup>
import { ref, reactive } from 'vue';

const name = ref('Amelia');

name.value = 'Damian';

const user = reactive({name: 'Amelia', surname: 'Staszczyk'});
user.surname = 'Nowak';

const selectedColor = ref();

</script>

<template>
  <div>
    <h1>{{ name }}</h1>
    <input type="text" v-bind:value="name" v-on:input="(event) => { name = event.target.value; }"/>
    <input type="text" v-model="name" :input="(event) => { name = event.target.value; }"/>
    <ul>
      <li>{{ user.name }}</li>
      <li>{{ user.surname }}</li>
    </ul>
    <select v-model="selectedColor" :on-change="(event) => {selectedColor = event.target.value;}">
      <option value="red">red</option>
      <option value="blue">blue</option>
      <option value="green">green</option>
    </select>
    <p>Wybrany kolor: 
      <span :style="{color: selectedColor}">{{ selectedColor }}</span>
    </p>
  </div>
</template>