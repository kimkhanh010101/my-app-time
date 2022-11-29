<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    @item-completed="markComplete"
    @delete-item="deleteTodo"
  />
</template>

<script>
import { ref } from 'vue'

// import { v4 as uuidv4 } from 'uuid'
import axios from 'axios'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'

export default {
  name: 'Todos',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])

    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'http://jsonplaceholder.typicode.com/todos?_limit=5'
        )
        // console.log(res.data)
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getAllTodos()

    const markComplete = id => {
      todos.value = todos.value.map(todo => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }

    const deleteTodo = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch (error) {
        console.log(error)
      }

      //   todos.value = todos.value.filter(todo => todo.id !== id)
    }

    const addTodo = newTodo => {
      todos.value.push(newTodo)
    }

    return {
      todos,
      markComplete,
      deleteTodo,
      addTodo
    }
  }
}
</script>

<style></style>
