
<template>

      <WikiItem v-for="(item, index) in objArticles" :key="index" :item="item"/>
    

</template>
  


<script setup>

import { defineProps, ref } from 'vue';

import WikiItem from './WikiItem.vue';

const props = defineProps(['objArticles']);


</script>

  


  
<style scoped>
  .container {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    font-size: 3rem;
  }
</style>