<template>
    <div class="rezult">
        <h2 class="rezult-title">{{ title }}</h2>
        <p class="rezult-content">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Veritatis optio, eum eius quod voluptates consequatur ad error tenetur quaerat cum odit temporibus in! Tenetur ullam expedita excepturi accusantium doloremque quas!</p>
        <p class="rezult-date">{{ date }}</p>
        <a class="rezult-link" :href="link">Ссылка на статью</a>
    </div>
</template>


<script setup> 

import {defineProps} from "vue";

const props = defineProps(['title', 'content', 'date', 'link']);



</script>


<style>

.rezult {
      margin-top: 15px;
      display: flex;
      gap:15px;
      max-width:500px;
      flex-wrap:wrap;
  }



</style>


