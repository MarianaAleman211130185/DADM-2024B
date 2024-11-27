<script setup>
import PlanPickerItem from './PlanPickerItem.vue';
import { onMounted, ref } from 'vue';
//Creando una referencia reactiva para almacenar el plan seleccionado
const selectedPlan = ref(null)
const plans = ref(['El cafetero', 'El chelero', 'El intelectual'])
const selectPlan = (name) => {
  //Almacenar el plan seleccionado
  selectedPlan.value=name;

  //console.log(name)
}

const plansWrapper = ref(null);

//Intentando obtener la referencia al elemento .plans
console.log("Termina de ejecutar el script setup 🎉")

//Registrando el hook mounted
onMounted(()=>{
  console.log("El componente PlanPikcker se ha montado")
  console.log("plansWrapper.value")
})
</script>

<template>
  <div ref="plansWrapper" class="plans">
    <PlanPickerItem 
    v-for="plan in plans" 
    :key="plan" 
    :name="plan" 
    @select="selectPlan"
    :select-plan="selectedPlan" />
  </div>


</template>

<style scoped></style>