<template>
  <div @click="selectPlan" class="plan">
    <div class="description">
      <span class="title">{{ name }} {{ selected ? '🦋' : ''}}
      </span>
    </div>
  </div>
</template>

<script setup>
//Importacion de la funcion ref
import { ref } from 'vue';

// Usando un macro para definir las props
//defineProps(['name', 'planIcon']);
const props = defineProps({
name :{
type : String,
requiered : true,
}
});
//Define event
const emit = defineEmits(['select']);
//Variable que permite recordar si el plan ha sido seleccionado
const selected = ref(false)
// Funcion que permite cambiar el estado de la variable
const selectPlan = () => {
selected.value = true;
//Emitir que el evento a sido seleccionado 
emit('select', props.name);
}
</script>

<style scoped>

</style>