
<template>
    <div class="container">
      <WikiItem v-for="(emoji, index) in emojis" :key="index" :emoji="emoji"/>
    </div>
</template>
  


<script setup>

import { defineProps, ref, watch } from 'vue';

import WikiItem from './WikiItem.vue';

const props = defineProps(['emojis']);


</script>

  


  
<style scoped>
  .container {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    font-size: 3rem;
  }
</style>