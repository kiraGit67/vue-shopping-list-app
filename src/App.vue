<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')

const items = ref([
  { id: 1, count: 10, label: '10er-Packs DVDs' },
  { id: 2, count: 25, label: 'DVD Labels' },
  { id: 3, count: 40, label: 'USB-Sticks' }
])
</script>

<template>
  <h1>{{ header }}</h1>
  <ul>
    <li v-for="({ id, count, label }, index) in items" :key="id">
      [{{ index }}] {{ id }}) {{ count }} {{ label }}
    </li>
  </ul>
</template>
