<template>
  <div class="todo-item">
    <li>
      <label class="todoList_label">
        <input class="todoList_input" type="checkbox" :checked="completed" @change="finishFromList" />
        <span :class="{ 'completed-text': completed }">{{ name }}</span>
      </label>
      <span @click.stop="removeTodo" class="remove-button">X</span>
    </li>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const { id, name, completed } = defineProps({
  id: Number,
  name: String,
  completed: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['emitFinishFromList', 'emitRemoveItem']);

const finishFromList = () => {
  emit('emitFinishFromList', { id, name, completed });
};

const removeTodo = () => {
  console.log('removeTodo id:', id);
  emit('emitRemoveItem', id);
};
</script>

<style scoped>
.completed-text {
  text-decoration: line-through;
  color: #9f9a91;
}

.todo-item {
  position: relative;
}

.remove-button {
  margin-left: 17px;
  display: block;
  font-size: 16px;
  color: #333;
  background: yellow;
  cursor: pointer;
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  opacity: 0;
  transition: opacity 0.2s;
}

.todo-item:hover .remove-button {
  opacity: 1;
}
</style>
