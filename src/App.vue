<template>
  <div class="container m-5">
    <div class="card">
      <div class="card-body">
       <h5 class="card-title text-center mb-3">Simple Todo App</h5> 
       <div class="row content-justify-center">
          <div class="col-sm-10">
            <input v-model="todo" type="text" class="form-control" @keyup.enter="add">
          </div>
          <div class="col-sm-2">
            <button class="btn btn-success" @click="add">Add</button>
          </div>

          <list :todos="list" @deleteTodo="deleteTodo" @doneTodo="doneTodo"/>
          <small> Total Todo : {{ totalTodo }}</small>
       </div>
      </div>
    </div> 
  </div>
</template>

<script>
import { computed, onMounted, reactive, ref, toRefs } from 'vue'
import List from './components/List.vue'
export default {
  components: { List },
  setup() {
    const todo = ref('')
    const todos = reactive({
      list: []
    })

    onMounted(() => {
      todos.list = JSON.parse(localStorage.getItem('todos'))
    })

    const totalTodo = computed(() => {
      return todos.list.length
    })

    const add = () => {
      todos.list.unshift({
        activity: todo.value,
        isDone: false
      })
      todo.value = ''
      saveToLocalStorage()
    }

    const deleteTodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index != todoIndex) {
          return item
        }
      })
      saveToLocalStorage()
    }

    const doneTodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true
        }

        return item
      })
      saveToLocalStorage()      
    }

    const saveToLocalStorage = () => {
      localStorage.setItem('todos', JSON.stringify(todos.list))      
    }

    return {
      todo,
      ...toRefs(todos),
      totalTodo,
      add,
      deleteTodo,
      doneTodo, 
    }
  }
}
</script>

<style>

</style>