<script setup>
import { ref, computed } from 'vue'

// Modelo
const header = ref('App lista de compras')
const items = ref([
  //---Items------
  //Item-Model
  { id: '0', label: '10 bolillos', purchased: false, priority: false },
  { id: '1', label: '1 lata frijoles', purchased: true, priority: true },
  { id: '2', label: '1 chelas', purchased: false, priority: false },
  { id: '3', label: '1 Nutella', purchased: true, priority: true }
])

// Item-Method
const saveItems = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value })
  // Limpiar la entrada
  newItem.value = ''
}
const newItem = ref('')
const newItemPriority = ref('false')
const editing = ref(true)
const activateEdition = (activate) => {
  editing.value = activate
}
// Alternando estado de compra del item
const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
// Propiedad computada para contar caracteres de entrada
const characterCount = computed(() => {
  return newItem.value.length
})
// Creando propiedad computada que invierte items de la lista
const reversedItems = computed(() => [...items.value].reverse())
</script>
<template>
  <div class="header">
    <h1>
      <i class="material-icons shopping-cart-icon">local_mall</i>
      {{ header }} <span style="color: blue">{{ newItemPriority }}</span>
    </h1>
    <button v-if="editing" class="btn" @click="activateEdition(false)">Cancelar</button>
    <button v-else class="btn btn-primary" @click="activateEdition(true)">Agregar Articulo</button>
  </div>
  <!-- Agrupando Entradas de usuario -->
  <form class="add-item form" v-if="editing" v-on:submit.prevent="saveItems()">
    <!-- Entrada de texto-->
    <input type="text" placeholder="Agregar articulo" v-model.trim="newItem" />
    <!-- Contador -->
    <p class="counter">
      {{ characterCount }} / 200
    </p>
    <!-- Radio Buttons -->
    <label>
      <input type="radio" value="low" v-model="newItemPriority" />
      Alta Prioridad
    </label>
    <!-- Boton -->
    <button :disabled="newItem.length === 0" class="btn btn-primary">Salvar Articulo</button>
  </form>
  <!-- Listas-->
  <ul>
    <li
      v-for="({ id, label, purchased }, index) in reversedItems"
      @click="togglePurchased(reversedItems[index])"
      :key="id"
      :class="{ strikeout: purchased, priority: highPriority }"
    >
      ⚜ {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0">🥀 NO HAY ELEMENTOS AGREGADOS</p>
</template>
<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
.counter {
  font-size: 0.9rem;
  color: #666;
}
</style>