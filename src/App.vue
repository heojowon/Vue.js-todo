<template>
  <div id="app">
    <div class="container">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">Todo List</h1>

        <div class="text-right mb-2">
          <button type="button" class="btn btn-sm" @click="changeCurrentState('active')">TODO</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('done')">DONE</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('all')">ALL</button>
        </div>

        <input type="text" class="form-control mb-3" v-model="userInput" @keyup.enter="addNewTodo">

        <div class="list-group mb-4">
          <template v-for="todo in activeTodoList">
            <todo
                    :label="todo.label"
                    @click="toggleTodoState(todo)"
            />
          </template>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo'

export default {
  name: 'app',
  data() {
    return {
      userInput: '',
      todoList: [],
      currentState: 'active'
    }
  },
  computed: {
    activeTodoList() {
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState)
    },
  },
  methods: {
    changeCurrentState(state) {
      this.currentState = state
    },
    addNewTodo() {
      this.todoList.push({
        label: this.userInput,
        state: 'active'
      }),
      this.userInput = ''
    },
    toggleTodoState(todo) {
      todo.state = todo.state === 'active' ? 'done' : 'active'
    },
  },
  components: {
    Todo
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
