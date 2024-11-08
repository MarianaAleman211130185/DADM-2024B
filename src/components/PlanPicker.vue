<script setup>
import PlanItem from './PlanItem.vue';
import { ref } from 'vue'
const plans = ref(['El cafetero', 'El chelero', 'El intelectual'])
</script>
<template>
  <div class="plans">
    <PlanItem v-for="plan in plans" :key="plan" :name="plan" />
  </div>
</template>

<style lang="scss" scoped></style>
