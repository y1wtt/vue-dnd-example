<script setup lang="ts">
import { computed } from 'vue'
import { Drag, DropList } from 'vue-easy-dnd'

const props = withDefaults(
  defineProps<{
    modelValue: Array<any>
  }>(),
  {
    modelValue: () => new Array<String>(),
  }
)

const emit = defineEmits<{
  (e: 'update:modelValue', items: Array<any>): void
}>()

const items = computed({
  get: () => props.modelValue,
  set: (value) => {
    emit('update:modelValue', value)
  },
})

const onInsert = (event: { index: number; data: string }) => {
  items.value.splice(event.index, 0, event.data)
}

const onCut = (event: { index: number; data: string }) => {
  items.value.splice(items.value.lastIndexOf(event.data), 1)
  console.log(event)
}
</script>

<template>
  <drop-list
    :items="items"
    @insert="onInsert"
    @reorder="$event.apply(items)"
    mode="cut"
    class="kanban"
  >
    <template v-slot:item="{ item }">
      <drag class="item" :data="item" :key="item" @cut="onCut">{{ item }}</drag>
    </template>
    <template v-slot:feedback="{ data }">
      <div class="item feedback" :key="data + 'feedback'">{{ data }}</div>
    </template>
  </drop-list>
</template>

<style scoped>
.kanban {
  margin: 0 20px;
  min-height: 10px;
  min-width: 250px;
}
.item {
  padding: 20px 100px;
  margin: 10px;
  background: #0352fc;
  text-align: center;
}
</style>
