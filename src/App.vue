<script setup lang="ts">
import Kanban from './components/Kanban.vue'
import { ref } from 'vue'

const strings = ref(['item1', 'item2', 'item3', 'item4', 'item5'])
const numbers = ref([1, 2, 3, 4, 5])
</script>

<template>
  <Kanban v-model="strings"></Kanban>
  <Kanban v-model="numbers"></Kanban>
</template>

<style scoped></style>
