<template>
  <div>
    <br />
    <TodoForm v-if="!todoToEdit" @add-todo="addTodo"></TodoForm>
    <TodoEdit v-else :todo="todoToEdit" @save-edit="updateTodo" @cancel-edit="todoToEdit = null"></TodoEdit>
    <label>
      <input type="checkbox" v-model="filter.showDone" />
      Erledigt
    </label>
    <TodoList :todos="filter ? filteredTodos : todos" @delete-todo="deleteTodo" @edit-todo="editTodo"
      @save-edit="updateTodo"></TodoList>
  </div>
</template>

<script>
import TodoForm from '@/components/TodoForm.vue'
import TodoList from '@/components/TodoList.vue'
import TodoEdit from '@/components/TodoEdit.vue'

export default {
  name: 'HomeView',

  components: {
    TodoForm,
    TodoList,
    TodoEdit,
  },
  data() {
    return {
      todoToEdit: null,
      todos: [],
      filter: { showDone: false, date: null },
    }
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) => {
        const matchDone = todo.done === this.filter.showDone

        return matchDone
      })
    },
  },
  methods: {
    addTodo(todo) {
      this.todos.push({
        id: Math.floor(Math.random() * 10000) + 1,
        text: todo.text,
        date: todo.date,
        done: false,
      })
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    editTodo(todo) {
      this.todoToEdit = {
        id: todo.id,
        text: todo.text,
        date: todo.date,
        done: todo.done,
      }
    },
    updateTodo(updatedTodo) {
      const index = this.todos.findIndex((todo) => todo.id === updatedTodo.id)
      this.todos.splice(index, 1, updatedTodo)
      localStorage.setItem('todos', JSON.stringify(this.todos))
      this.todoToEdit = null
    },
    testFunction() {
      const name = 'Erdem'
      const names = ['Erdem', 'Tamer'] // names[0], names[1]
      const person = { name: 'Erdem', hobby: 'Naruto' } // person.name
      const persons = [{ name: 'Erdem', hobby: 'Naruto' }, { name: 'Tamer', hobby: 'One Piece' }]
    }
  },
  mounted() {
    const todos = localStorage.getItem('todos')
    if (todos) {
      this.todos = JSON.parse(todos)
    }
  }
}
</script>

<style></style>
