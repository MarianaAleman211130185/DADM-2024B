<script setup>
import { ref } from 'vue'
const header = ref('App lista de compras')
const items = ref([
  { id: '1', label: '10 bolillos' },
  { id: '2', label: '1 lata de frijoles' },
  { id: '3', label: '1 chela' },
  { id: '4', label: '1 nutella' },
  { id: '5', label: '1 lata de atun' },
  { id: '6', label: '1 pcgamer' }
])
const newItem = ref('')
const newItemHighPriority = ref(false)
const addItem = () => {
  if (newItem.value.trim()) {
    items.value.push({
      id: items.value.length + 1,
      label: newItem.value,
      priority: newItemHighPriority.value ? 'high' : 'low'
    })
    newItem.value = ''
    newItemHighPriority.value = false
  }
}
</script>
<template>
  <h1>
    <i class="material-icons shopping-cart-icon">local_mall</i>
    {{ header }}
  </h1>
  <div>
    <form @submit.prevent="addItem" class="add-item form">
      <input
        v-model.trim="newItem"
        type="text"
        placeholder="Add Item"
      />
      <label>
        <input type="checkbox" v-model="newItemHighPriority" />
        High Priority
      </label>
      <button class="btn btn-primary">
        Save Item
      </button>
    </form>
  </div>
  <ul>
    <li v-for="item in items" :key="item.id">
      🛒{{ item.label }} ({{ item.priority }})
    </li>
  </ul>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>