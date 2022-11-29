<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input
      type="checkbox"
      :checked="todoProps.completed"
      @change="markItemCompleted"
    />
    {{ todoProps.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
//import { ref } from 'vue'

export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.todoProps.id)
    }

    const deleteItem = () => {
      context.emit('delete-item', props.todoProps.id)
    }

    return {
      markItemCompleted,
      deleteItem
    }
  }
}
</script>

<style>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  font-size: 1.1rem;
  border-bottom: 1px #ccc dotted;
}

.del-btn {
  margin-right: 12px;
  margin-top: -8px;
  font-size: 1.1rem;
  padding: 8px;
  border-radius: 5px;
  color: #fff;
  background: rgb(216, 5, 5);
  border: 1px solid rgb(216, 5, 5);
  cursor: pointer;
  float: right;
}

.is-completed {
  text-decoration: line-through;
}
</style>
