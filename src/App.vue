<script setup>
// doc 14
import { ref, reactive } from 'vue';

const name = ref('Amelia');

name.value = 'Damian';

const user = reactive({ name: 'Amelia', surname: 'Staszczyk' });
user.surname = 'Nowak';

const selectedColor = ref();

//doc 15
//const todo = ref(['Zrobić matmę', 'Odkurzyć pokój', 'Wynieść śmieci']);
const todo = ref([
  {
    text: "Zrobić matmę",
    finished: false
  },
  {
    text: "Odkurzyć pokój",
    finished: true
  },
  {
    text: "Wynieść śmieci",
    finished: false
  },
]);
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
    <input type="text" v-bind:value="name" v-on:input="(event) => { name = event.target.value; }" />
    <input type="text" v-model="name" :input="(event) => { name = event.target.value; }" />
    <ul>
      <li>{{ user.name }}</li>
      <li>{{ user.surname }}</li>
    </ul>
    <select v-model="selectedColor" :on-change="(event) => { selectedColor = event.target.value; }">
      <option value="red">red</option>
      <option value="blue">blue</option>
      <option value="green">green</option>
    </select>
    <p>Wybrany kolor:
      <span :style="{ color: selectedColor }">{{ selectedColor }}</span>
    </p>
  </div>

  <!--doc 15-->
  <div>
    <ul>
      <!-- <li v-for="(task, index) in todo">{{ index }} - {{ task }}</li>

      <li v-for="(task, index) in todo" v-key="index">{{ task }}</li> -->

      <!-- <li
      v-for="(task, index) in todo"
      v-key="index"
      v-show="task.finished == false"
    >{{ task.text }}</li> -->

      <!-- <template v-for="task in todo">  
      <li v-if="task.finished == false">
        {{ task.text }}
        <input :value="task.finished" type="checkbox">
      </li>
    </template> -->

      <!-- <template v-if="todo[0]">
        <template v-for="task in todo">
          <li v-if="task.finished == false">
            {{ task.text }}
            <input v-model="task.finished" type="checkbox">
          </li>
          <li v-else>
            <s>{{ task.text }}</s>
            <input v-model="task.finished" type="checkbox">
          </li>
        </template>
      </template>
      <template v-else>
        <p>Brak zadań do zrobienia</p>
      </template> -->

        <template v-for="task in todo">
          <li v-if="task.finished == false">
            {{ task.text }}
            <input v-model="task.finished" type="checkbox">
          </li>
          <li v-else>
            <s style="color: darkgray">{{ task.text }}</s>
            <input v-model="task.finished" type="checkbox">
          </li>
        </template>
      <template v-if="todo.every((task) => task.finished)">
        <p>Brak zadań do zrobienia</p>
      </template>


    </ul>
  </div>
</template>