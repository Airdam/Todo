<template>
  <div>
    <br />
    <TodoForm v-if="!todoToEdit" @add-todo="addTodo"></TodoForm>
    <TodoEdit
      v-else
      :todo="todoToEdit"
      @save-edit="updateTodo"
      @cancel-edit="todoToEdit = null"
    ></TodoEdit>
    <label>
      <input type="checkbox" v-model="filter.showDone" />
      Erledigt
    </label>
    <TodoList
      :todos="filter ? filteredTodos : todos"
      @delete-todo="deleteTodo"
      @edit-todo="editTodo"
    ></TodoList>
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
      nextId: 1,
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
        id: this.nextId,
        text: todo.text,
        date: todo.date,
        done: false,
      })
      this.nextId++
      // funzt im locoalstorage nicht
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
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
      this.todoToEdit = null
    },
  },
}
</script>

<style></style>
