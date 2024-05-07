<script setup>
import { ref, defineProps, onMounted } from "vue";
import "./styles/accordion.css"
import TodoItem from './TodoItem.vue';
import NewTask from "./NewTask.vue";
const props = defineProps(['title']);
const visible = ref(false);
const todoItems = ref([{ text: 'Initial todo item', finished: true }]);
function expose() {
    visible.value = true
}
function collapse() {
    visible.value = false;
}
function addNewItem() {
  const newText = prompt("Enter title:");
  todoItems.value.push({ text: newText, finished: false });
}
defineExpose({collapse});
</script>

<template>
    <section>
        <header class="title">
            <h1>{{ title }}</h1>
            <button class="toggle" v-if="!visible" @click='expose()'>&darr;</button>
            <button class="toggle" v-if="visible" @click='collapse()'>&uarr;</button>
        </header>
        <div class="tasks" v-if="visible">
            <TodoItem v-for="(item, index) in todoItems" :key="index" :text="item.text" v-model="item.finished" />
            <NewTask @create="addNewItem(todoItems)"></NewTask>
        </div>
    </section>
</template>
