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

const editing = ref(false)

//Methods
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, count: newCount.value, label: newItem.value })
  newCount.value = ''
  newItem.value = ''
}

const doEdit = (event) => {
  editing.value = event
  newCount.value = ''
  newItem.value = ''
}
</script>

<template>
  <header class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add New Item</button>
  </header>
  <form v-if="editing" class="add-item-form" @submit.prevent="saveItem">
    <input v-model="newCount" type="number" name="new-count" id="new-count" maxlength="4" />
    <input
      v-model.trim="newItem"
      type="text"
      name="new-item"
      id="new-item"
      placeholder="Add new item"
      :disabled="newItem.length > 50"
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
    <button :disabled="newItem.length === 0 || newCount.length === 0" class="btn btn-primary">
      Save Item
    </button>
  </form>
  <p>{{ newCount }} {{ newItem }}</p>
  <ul>
    <li v-for="({ id, count, label }, index) in items" :key="id">
      [{{ index }}] {{ id }}) {{ count }} {{ label }}
    </li>
  </ul>
</template>
