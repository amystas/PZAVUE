<script setup>
const props = defineProps({
    'task' :String, /*'completed' :Number*/
});
const model = defineModel();
const emit = defineEmits(['changed']);
</script>

<template>
    <li>
        <!-- <input type="checkbox" :checked="completed" @click="emit('changed', completed)"> -->
        <!-- <input type="checkbox" v-model="model" @click="emit('changed', event.target.value)"> -->
        <button @click="model = !model">{{ model ? 'Odznacz' : 'Ukończ' }}</button>
        {{props.task}}
    </li>
</template>