<template>
  <form @submit="addItem">
    <input
      class="input-text"
      type="text"
      placeholder="Thêm công việc mới..."
      v-model="title"
    />
    <input type="submit" value="+ Thêm" class="add-btn" />
  </form>
</template>

<script>
import { ref } from 'vue'

import { v4 as uuidv4 } from 'uuid'

export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')
    const addItem = event => {
      event.preventDefault()

      const newItem = {
        id: uuidv4(),
        title: title.value,
        completed: false
      }

      context.emit('add-todo', newItem)

      title.value = ''
    }
    return {
      title,
      addItem
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
}

input[type='text'] {
  flex: 10;
  padding: 5px;
}

input[type='submit'] {
  flex: 2;
}
.input-text {
  border: 1px solid rgb(138, 135, 135);
  border-radius: 5px;
  font-size: 1.1rem;
  margin-right: 4px;
}

.add-btn {
  color: #fff;
  background: rgb(20, 202, 4);
  font-size: 1.2rem;
  font-weight: 600;
  padding: 12px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
}
</style>
