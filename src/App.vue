<template>
  <button @click="showTimer =!showTimer">Afficher /masquer</button>
  <Timer v-if="showTimer"/>

  <form action="" @submit.prevent="addTodo" class="m-10">

    <fieldset>
      <label>
        <input type="text" v-model="newTodo" placeholder="Tâche à effectuer"
          class="p-2 bg-green-50 focus:border-2 focus:border-red-500 border-l-2 border-b-2 border-t-2" />
      </label>
      <label>
        <button :disabled="newTodo.length === 0"
          class="bg-green-500 text-white px-4 py-2 mr-5 border-green-500 border-r-2 border-b-2 border-t-2 rounded-r-md hover:bg-green-600 disabled:bg-green-300 disabled:border-green-300">
          Ajouter une tâche
        </button>
      </label>
    </fieldset>

  </form>
  <div class="m-10">

    <div v-if="todos.length === 0">
      Vous n'avez pas de tâches à faire 🥺
    </div>
    <div v-else>
      <ul>
        <li class="list-disc ml-6 mt-2" v-for="todo in sortedTodos" :key="todo.date"
          :class="{ 'line-through': todo.completed, 'opacity-100': todo.completed }">

          <Checkbox :label="todo.title" class="text-green-900"/>

        </li>


      </ul>

      <label class="block mt-4">
        <input type="checkbox" v-model="hideCompleted" class="mr-2" /> Masquer les tâches terminées
      </label>
      <button @click="sortTodos"
        class="bg-green-500 text-white px-4 py-2 rounded mt-2 hover:bg-green-600">Trier</button>
    </div>
    <br>
    <div v-if="remainingTodos > 0" class="text-3xl"> {{ remainingTodos }} tâche{{ remainingTodos > 1 ? "s" : "" }} à
      faire

    </div>

  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import Checkbox from '/components/Checkbox.vue';
import Timer from '/components/Timer.vue';


const newTodo = ref('');
const todos = ref([]);
const hideCompleted = ref(false); // Ajout de hideCompleted
const showTimer = ref(true);



onMounted(() => {
  fetch('https://jsonplaceholder.typicode.com/todos')
    .then(response => response.json())
    .then(val => todos.value = val.map(
      todo => ({
      ...todo, date: todo.id
      }))
    ); 
});


const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now(),
  });
  newTodo.value = '';
};

const sortTodos = () => {
  todos.value.sort((a, b) => a.title.localeCompare(b.title));
};

const deleteTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo);
};



// Propriété Dérivée

const sortedTodos = computed(() => {


  const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)

  if (hideCompleted.value === true) {
    return sortedTodos.filter(t => t.completed === false)
  }
  return sortedTodos;
});

const remainingTodos = computed(() => {
  return todos.value.filter(t => t.completed === false).length;
})




</script>
