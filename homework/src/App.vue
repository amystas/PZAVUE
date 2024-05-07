<script setup>
import { ref } from "vue";
import Accordion from './Accordion.vue';
import NewList from './NewList.vue';
import "./styles/app.css";

const accordions = ref([{ title: 'Tasks 1' }, { title: 'Tasks 2' }]);
const accordionsList = ref([])

function collapseAll() {
  accordionsList.value.forEach(element => {
    element.collapse();
  });
}

function addNewList(title) {
  accordions.value.push({ title: title });
}
</script>

<template>
  <aside>
    <NewList @addList="addNewList($event)"></NewList>
    <button @click="collapseAll">Collapse All</button>
  </aside>
  <Accordion class="accordion" v-for="(item, index) in accordions" :key="index" :title="item.title" ref="accordionsList"/>
</template>
