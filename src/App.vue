<script setup>
import { ref, computed } from 'vue'

const header = ref('Shopping List App')

const items = ref([
  { id: 1, count: 10, label: '10er-Packs DVDs', purchased: true, highPriority: false },
  { id: 2, count: 25, label: 'DVD Labels', purchased: false, highPriority: false },
  { id: 3, count: 40, label: 'USB-Sticks', purchased: false, highPriority: true }
])

const newItem = ref('')
const newCount = ref('')
const newItemHighPriority = ref(false)

const editing = ref(false)

//Computed Properties
const characterCount = computed(() => {
  return newItem.value.length
})

const reversedItems = computed(() => {
  return [...items.value].reverse()
})

//Methods
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    count: newCount.value,
    label: newItem.value,
    purchased: false,
    highPriority: newItemHighPriority.value
  })
  newCount.value = ''
  newItem.value = ''
  newItemHighPriority.value = ''
}

const doEdit = (event) => {
  editing.value = event
  newCount.value = ''
  newItem.value = ''
  newItemHighPriority.value = ''
}

const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <header class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" :class="{ 'btn-cancel': editing }" @click="doEdit(false)">
      Cancel
    </button>
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
      :disabled="characterCount > 50"
      :class="{ invalid: characterCount > 50 }"
    />
    <p class="counter">
      <span :class="{ invalid: characterCount > 50 }">{{ characterCount }}</span
      >/50
    </p>
    <label for="high-priority">
      <input
        v-model="newItemHighPriority"
        type="checkbox"
        name="high-priority"
        id="high-priority"
        :class="{ invalid: characterCount > 50 }"
        :disabled="characterCount > 50"
      />
      High Priority
    </label>
    <button
      :disabled="characterCount === 0 || characterCount > 50 || newCount.length === 0"
      class="btn btn-primary"
    >
      Save Item
    </button>
  </form>
  <p>{{ newCount }} {{ newItem }}</p>
  <ul>
    <li
      v-for="({ id, count, label, purchased, highPriority }, index) in reversedItems"
      :key="id"
      class="static-class"
      :class="{ strikeout: purchased, priority: highPriority }"
      @click="togglePurchased(reversedItems[index])"
    >
      [{{ index }}] {{ id }}) {{ count }} {{ label }}
    </li>
  </ul>
</template>
