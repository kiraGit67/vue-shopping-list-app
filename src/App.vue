<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')

const items = ref([
  { id: 1, count: 10, label: '10er-Packs DVDs' },
  { id: 2, count: 25, label: 'DVD Labels' },
  { id: 3, count: 40, label: 'USB-Sticks' }
])

const newItem = ref('')
const newCount = ref('')
//const newItemPriority = ref('low')
const newItemHighPriority = ref(false)
</script>

<template>
  <header>
    <h1>{{ header }}</h1>
  </header>
  <form class="add-item-form">
    <input v-model="newCount" type="number" name="new-count" id="new-count" maxlength="4" />
    <input
      v-model.trim="newItem"
      type="text"
      name="new-item"
      id="new-item"
      placeholder="Add new item"
    />
    <!--
    <label for="priority">
      Priority:
      <select v-model="newItemPriority" name="priority" id="priority">
        <option value="low">Low</option>
        <option value="high">High</option>
      </select>
    </label>
    -->
    <label for="high-priority">
      <input
        v-model="newItemHighPriority"
        type="checkbox"
        name="high-priority"
        id="high-priority"
      />
      High Priority
    </label>
  </form>
  <ul>
    <li v-for="({ id, count, label }, index) in items" :key="id">
      [{{ index }}] {{ id }}) {{ count }} {{ label }}
    </li>
  </ul>
</template>
