<script setup>
import { ref } from 'vue';

const message = ref('Hello Vue 3!');

</script>

<template>
  <div>
    <h1>{{ message }}</h1>
    <input type="text" v-model="message"/>
  </div>
</template>