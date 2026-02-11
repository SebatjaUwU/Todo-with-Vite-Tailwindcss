<script setup>

import { ref } from 'vue'

let id = 0

const newTodo = ref({ text: '', priority: '' })
const todos = ref([
    { id: id++, text: 'Learn Vue.js', priority: 'High' },
    { id: id++, text: 'Build a to-do app', priority: 'Medium' },
    { id: id++, text: 'Master Tailwind CSS', priority: 'Low' },
])

function addTodo(){
    todos.value.push({ id: id++, text: newTodo.value.text, priority: newTodo.value.priority })
    newTodo.value = { text: '', priority: 'Low' }
}

function removeTodo(todo){
    todos.value = todos.value.filter(item => item.id !== todo.id)
}

</script>
<template>
    <div class="mt-6 text-center mb-12 text-primary text-3xl font-bold ">
        <p>
            To do List
            <img src="../assets/todo.svg" class="w-16 h-16 mx-auto" alt="Vue logo" />
        </p>

    </div>
    <div class="text-center flex flex-col items-center justify-center">
        <form @submit.prevent="addTodo">
            <input v-model="newTodo.text" type="text" required="" placeholder="Add a new task"
                class="border-2 border-gray-300 rounded-lg px-4 py-2 mr-4 mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500" />
            <select v-model="newTodo.priority"
                class="border-2 border-gray-300 rounded-lg px-4 py-2 mr-4 mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
                name="" id="">
                <option selected value="Low">Low</option>
                <option value="Medium">Medium</option>
                <option value="High">High</option>
            </select>
            <button type="submit"
                class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition-colors duration-300">Add
                Task</button>

        </form>
    </div>

    <div class="mt-6 text-center mb-12 text-primary text-3xl font-bold ">
        <p>
            Tasks
        </p>  
    </div>
<!-- 
    <ul>
        <li v-for="todo in todos" :key="todo.id">
            {{ todo.text }} - {{ todo.priority }}
            <button @click="removeTodo(todo)" class="ml-4 bg-red-500 text-white px-2 py-1 rounded hover:bg-red-600 transition-colors duration-300">
                Remove

            </button>

        </li>
    </ul> -->

    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-6">
            <div v-for="todo in todos" :key="todo.id" class="bg-white rounded-lg shadow p-4 hover:bg-primary shadow-2xl transition-colors duration-300 group">
                <h3 class="text-lg font-semibold mb-2 group-hover:text-white">{{ todo.text }}</h3>
                <p class="text-gray-600 mb-4 group-hover:text-white ">Priority: {{ todo.priority }}</p>
                <button @click="removeTodo(todo)"
                    class="bg-red-500 text-white px-2 py-1 rounded hover:bg-red-600 transition-colors duration-300">
                    Remove
                </button>
            </div>
    </div>
 
</template>
