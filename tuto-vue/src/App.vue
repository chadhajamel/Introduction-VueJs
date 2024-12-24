<template>
  <form @submit.prevent="addTodo">
    <input type="text" v-model="newTodo" placeholder="Tache a effectuer"/>
    <button type="submit" :disabled="newTodo.length===0">Ajouter</button>

  </form>
  <div  v-if="todos.length===0">
    vous n'avez pas de tâches
  </div>
  <div v-else="todos.length>0">
    <ul>
      <li v-for="todo in sortedTodos()" :key="todo.date">
        <input type="checkbox" v-model="todo.done"/>
        <span :style="{textDecoration: todo.done ? 'line-through' : 'none'}">{{todo.title}}</span>

        <!-- autre methode -->
        <!-- <checkbox :label="todos.title" ></checkbox> -->
      </li>
    </ul>

    <div>
      <label>  
        <input type="checkbox" v-model="hideComplete">Masquer les taches completes
        </input>
      </label>
    </div>

    <!-- checkbox with componenrt input -->
    <checkbox label="bonjour chadhou" ></checkbox>

    <!-- checkbox with componenrt evenemet -->
    <checkbox label="event" @checked="console.log('ggg')" @unchecked="console.log('ttt')" 
    ></checkbox>





  </div>

</template>

<script setup> 
import { ref } from 'vue'
import checkbox from './components/checkbox.vue'
const newTodo = ref('')
const todos = ref([
  {title:'Apprendre Vue 3', done:true, date: Date.now()},
  {title:'Apprendre Vue Router', done:false, date: Date.now()},
  {title:'Apprendre VueX', done:false, date: Date.now()}
])
const hideComplete = ref(false) 

const addTodo = () => {
  todos.value.push({
    title:newTodo.value,
    done:false,
    date: Date.now()
    }
  )
  newTodo.value = ''
}

const  sortedTodos=()=>{
 const sortedTodo= todos.value.sort((a,b)=>
   a.done>b.done ? 1 : -1
  )
  if (hideComplete.value){
    return sortedTodo.filter(todo=>!todo.done)
  }
  return sortedTodo
}

</script>