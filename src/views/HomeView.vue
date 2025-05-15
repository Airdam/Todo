<template>
  <div class="min-h-screen w-full bg-gray-600 text-white flex justify-center items-top">
    <div class="w-full px-4">
      <h1 class="text-3xl flex justify-left mt-6 mb-6">Todo App</h1>

      <TodoForm v-if="!todoToEdit" @add-todo="addTodo" />
      <TodoEdit
        v-else
        :todo="todoToEdit"
        @save-edit="updateTodo"
        @cancel-edit="todoToEdit = null"
      />

      <div class="mb-4">
        <label class="flex items-center space-x-2">
          <input
            type="checkbox"
            v-model="filter.showDone"
            class="flex items-center size-4 m-2 p-2 text-red-500"
          />
          <span>Erledigt</span>
        </label>
      </div>

      <TodoList
        :todos="filter ? filteredTodos : todos"
        @delete-todo="deleteTodo"
        @edit-todo="editTodo"
        @save-edit="updateTodo"
      />
    </div>
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
    deleteTodo(todo) {
      // this.todos.splice(index, 1)
      this.todos = this.todos.filter((item) => item.id !== todo.id)
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
  },
  mounted() {
    const todos = localStorage.getItem('todos')
    if (todos) {
      this.todos = JSON.parse(todos)
    }
  },
}
</script>

<style></style>
