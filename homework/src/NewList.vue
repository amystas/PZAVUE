<script setup>
  const emit = defineEmits(['addList']);

  function addList() {
    const title = document.getElementById('title').value;
    emit('addList', title);
  }
</script>

<template>
  <form @submit.prevent="addList">
    <label for="title">Enter title: </label>
    <input type="text" name="title" id="title">
    <button type="submit">Add list</button>
  </form>
</template>
