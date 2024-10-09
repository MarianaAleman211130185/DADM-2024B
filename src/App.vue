<script setup>
import { ref } from 'vue'
// Modelo
const header = ref('App lista de compras')
const items = ref([
  //---Items------
  //Item-Model
  { id: '0', label: '10 bolillos', purchased: false, priority: false},
  { id: '1', label: '1 lata frijoles', purchased: true, priority: true},
  { id: '2', label: '1 chelas' , purchased: false, priority: false},
  { id: '3', label: '1 Nutella', purchased: true, priority: true}
])
// Item-Method
const saveItems = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value })
  // clean the input
  newItem.value = ''
}
const newItem = ref('')
const newItemPriority = ref('false')
const editing = ref(true)
const activateEdition = (activate) => {
  editing.value = activate
}
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
    <!-- Radio Buttos -->
    <label>
      <input type="radio" value="low" v-model="newItemPriority" />
      Alta Prioridad
    </label>
    <!-- Boton -->
    <button 
    :disabled="newItem.length === 0"
    class="btn btn-primary">Salvar Articulo</button>
  </form>
  <!-- Listas-->
  <ul>
    <li v-for="{label, id, purchased, priority} in items" 
    :key="id"
    :class="{ strikeout: purchased, priority: priority}">
    {{ priority ? "🔥" : "🛒" }} {{ label }}
  </li>
  </ul>
  <!-- Listas clases como arreglos-->
  <ul>
    <li v-for="{label, id, purchased, priority} in items" 
    :key="id"
    :class="[purchased ? 'strikeout': '', priority ? 'priority':'']">
    {{ priority ? "🔥" : "🛒" }} {{ label }}
  </li>
  </ul>
  <p v-if="items.length === 0">🥀 NO HAY ELEMENTOS AGREGADOS</p>
</template>
<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
