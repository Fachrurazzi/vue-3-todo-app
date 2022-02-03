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

          <list :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo"/>
          <small> Total Todo : {{ totalTodo }}</small>
       </div>
      </div>
    </div> 
  </div>
</template>

<script>
import List from './components/List.vue'
export default {
  components: { List },
  data() {
    return {
      todo: "",
      todos: []
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'))
  },
  computed: {
    totalTodo() {
      return this.todos.length
    }
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false
      })
      this.todo = ""
      this.saveToLocalStorage()
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item,index) => {
        if (index != todoIndex) {
          return item
        }
      })
      this.saveToLocalStorage()
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true
        }

        return item
      })
      this.saveToLocalStorage()
    },
    saveToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  }
}
</script>

<style>

</style>