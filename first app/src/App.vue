<script setup>
// doc 14
import { ref, reactive, computed, watch } from 'vue';
import TodoItem from './TodoItem.vue';
import TodoInput from './TodoInput.vue';

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
  {
    text: "Umówić wizytę",
    finished: false
  },
  {
    text: "Zetrzeć kurze",
    finished: false
  },
  {
    text: "Umyć naczynia",
    finished: false
  },
]);

// doc 16
name.value = 'Amelia';
const lastname = ref('Staszczyk');
const fullname = computed(() => name.value + ' ' + lastname.value);
const showWarning = ref(true);

function hideWarning() {
  showWarning.value = false;
}

function addTask() {
  todo.value.push({text: document.getElementById('newTaskText').value, finished: false});
}

const unfinishedTasksCount = ref(0);
watch(todo, (newValue) => {
	unfinishedTasksCount.value = newValue.filter(task => !task.finished).length;
  console.log(unfinishedTasksCount.value);
  if(unfinishedTasksCount.value < 4) {
    showWarning.value = false;
    console.log('no niby działa');
  }
}, { deep: true });


const completedTasks = computed(() => todo.value.filter(task => task.finished).length + '/' + todo.value.length);

// doc 17
function changeStatus(task, completed) {
  task.finished = !completed;
}
function addNewTask(text) {
  console.log('app.vue');
  todo.value.push({text: text, finished: false});
}

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
        <h4>Ukończono {{ completedTasks }} zadań</h4>
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
      <template v-if="showWarning">
        <p>Może byś coś z tego zrobił wreszczie</p>
        <button @click="hideWarning()">OK</button>
      </template>


    </ul>
    <label for="">Dodaj zadanie: </label>
    <input type="text" id="newTaskText" v-on:keyup.enter="addTask">
    <button @click="addTask">Dodaj</button>
  </div>

  <!-- doc 17 -->
  <div>
    <!-- <TodoItem v-for="task in todo" :task="task.text" :completed="task.finished" @changed="changeStatus(task, $event)"></TodoItem> -->
    <TodoItem v-for="task in todo" :task="task.text" v-model="task.finished" @changed="changeStatus(task, $event)"></TodoItem>
    <TodoInput @create="addNewTask($event)"></TodoInput>
  </div>

  <div>
    <h2>{{ fullname }}</h2>
  </div>
</template>