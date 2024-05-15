<template>
    <div class="rezult">
        <h2 class="rezult-title">{{ item.title }}</h2>
        <p class="rezult-content" v-html="stripHTML(item.snippet)"></p>
        <p class="rezult-date">{{ formatDate(item.timestamp) }}</p>
        <a class="rezult-link" target="_blank" :title="`http://ru.wikipedia.org/?curid=${item.pageid}`" :href="`http://ru.wikipedia.org/?curid=${item.pageid}`">Ссылка на статью</a>
    </div>
</template>


<script setup> 

import {defineProps} from "vue";

const props = defineProps(['item']);


const formatDate = (time) => {

    const date = new Date(time);
    return date.toLocaleString();

}

// const stripHTML = (html) => {
//     const doc = new DOMParser().parseFromString(html, 'text/html');
//     return doc.body.textContent || "";
// }

const stripHTML = (htmlString) => {
  const regex = /<[^>]*>/g;
  const correctSnippet = htmlString.replace(regex, "");

  let firstChar = correctSnippet.charAt(0);

  let upperFirstChar = firstChar.toUpperCase();

  let restOfString = correctSnippet.slice(1);

  let rezult = upperFirstChar + restOfString + "...";


  return rezult;
};




</script>


<style>

.rezult {
    border-radius: 4%;
    box-shadow: 0 4px 15px rgb(0 0 0 / 10%);
    padding: 15px;
    margin-top: 2rem;
    margin-bottom: 15px;
    display: flex;
    gap:15px;
    max-width:570px;
    flex-wrap:wrap;
    transition: all 0.2s;
}

.rezult:hover{
    cursor: pointer;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3); 
    transform: scale(1.03); 
}


a{
    color: #007bff;
}
a:hover{
    color: #7b9dc4;

}

@media (max-width: 600px) {
    .rezult{
        margin: 15px;
      
    }
    
  }




</style>


