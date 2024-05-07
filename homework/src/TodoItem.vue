<script setup>
    const props = defineProps(['text'])

    const finished = defineModel()
</script>

<template>
    <div>
        <input type="checkbox" name="" id="" v-model="finished">
        <label>{{ text }}</label>
    </div>
</template>