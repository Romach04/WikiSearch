<template>
  <div class="wrapper">

    <div class="container">
        <div class="search-box">
            <input class="search-input" type="text" placeholder="Введите запрос" v-model="searchText">
            <button class="search-button" @click="loadArticles()">Поиск</button>
        </div>

        <WikiItem :title="title" :content="content" :date="date" :link="link"/>
    </div>

  </div>
</template>



<script setup>

import { ref } from "vue";

import axios from 'axios'

import WikiItem from "./components/WikiItem.vue";
const searchText = ref('');

const errorMessage = ref('');
const listArticles = ref(['']);

const title = "Заголовок статьи"
const content = "Подзаголовок статьи"
const date = "15.04.32"
const link = "ffff"


async function loadArticles() {

  if (searchText.value) {
    try {
      const response = await axios.get(`/wiki/w/api.php?action=query&list=search&srsearch=${searchText.value}&format=json`);

      listArticles.value = response.data;


      if(listArticles.value.query.search.length === 0) {
        errorMessage.value = "Нет результатов";
      }
      
      console.log(listArticles.value.query.search);

    } catch (error) {
      console.error('Ошибка при выполнении запроса:', error);
    }
  }
}


</script>








<style scoped>
  .wrapper{
    max-width: 1280px;
    margin: 0 auto;
    font-weight: normal;
    min-height: 100vh;
  }

  .container{
    margin-top: 30px;
    box-shadow: 0 4px 15px rgb(0 0 0 / 10%);
    background-color: white;
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 6%;
  }

  .search-box {
    width: 90%;
    margin-top: 30px;
    display: flex;
    gap: 10px;
  }

  .search-input{
    flex: 1;
    padding: 10px;
    font-size: 16px;
  }

  .search-button{
      padding: 10px 20px;
      background-color: #007bff;
      color: #fff;
      border: none;
      cursor: pointer;
      font-size: 16px;
      transition: all 0.25s;
  }

  .search-button:hover{
    background-color: #6ca3df;

  }

  

  


</style>
