<script setup>
import planItem from './plan-item.vue';
import { ref } from 'vue';
const plans = ref(['El cafetero', 'El chelero', 'El intelectual']);
</script>
<template>
<div class="plans">
 <plan-item v-for="plan in plans" :key="plan" :name="plan" />
</div>
</template>

<style lang="scss" scoped>

</style>