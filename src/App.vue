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
const newItemHighPriority = ref(false)

//Methods
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, count: newCount.value, label: newItem.value })
  newCount.value = ''
  newItem.value = ''
}
</script>

<template>
  <header>
    <h1>{{ header }}</h1>
  </header>
  <form class="add-item-form" @submit.prevent="saveItem">
    <input v-model="newCount" type="number" name="new-count" id="new-count" maxlength="4" />
    <input
      v-model.trim="newItem"
      type="text"
      name="new-item"
      id="new-item"
      placeholder="Add new item"
    />
    <label for="high-priority">
      <input
        v-model="newItemHighPriority"
        type="checkbox"
        name="high-priority"
        id="high-priority"
      />
      High Priority
    </label>
    <button class="btn btn-primary">Save Item</button>
  </form>
  <p>{{ newCount }} {{ newItem }}</p>
  <ul>
    <li v-for="({ id, count, label }, index) in items" :key="id">
      [{{ index }}] {{ id }}) {{ count }} {{ label }}
    </li>
  </ul>
</template>
