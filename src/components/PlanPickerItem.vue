<template>
  <div @click="selectPlan" 
  class="plan"
  :class="{selected: isSelected}">
    <div class="description">
      <span class="title">{{ name }} {{ isSelected ? '🦋' : ''}}
      </span>
    </div>
  </div>
</template>

<script setup>
//Importamos la función para crear la propiedad computada
import { computed } from 'vue';

// Usando un macro para definir las props
//defineProps(['name', 'planIcon']);
const props = defineProps({
name :{
type : String,
requiered : true,
},
selectPlan: String
});
//Define event
const emit = defineEmits(['select']);
// Funcion que permite cambiar el estado de la variable
const selectPlan = () => {
//Emitir que el evento a sido seleccionado 
emit('select', props.name);
}
//Creando una propiedad computada para saber si el plan ha sido seleccionado
const isSelected = computed(()=>{
  return props.name === props.selectPlan;
});
</script>
<style scoped>

</style>