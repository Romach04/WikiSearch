<template>
  <div class="wrapper">

    <div class="container">
        <div class="search-box">
            <input class="search-input"  type="text" placeholder="Введите запрос" v-model="searchText" @keyup.enter="loadArticles()">
            <button class="search-button" @click="loadArticles()">Поиск</button>
        </div>

        <div v-if="loading" class="spinner">

          <div>
            <VueSpinner  size="60" color="blue"/>
          </div>

        </div>

        <div class="error-message" v-else-if="objArticles && objArticles.length === 0">Нет результатов</div>
        
        <WikiItemList v-else :objArticles="objArticles"/>

    </div>

  </div>
</template>



<script setup>

import { ref } from "vue";

import axios from 'axios'
import {VueSpinner} from 'vue3-spinners';

import WikiItemList from "./components/WikiItemList.vue";
const searchText = ref('');

const loading = ref(false);

const listArticles = ref(['']);

const objArticles = ref(null);



async function loadArticles() {
  
  loading.value = true;

  if (searchText.value) {
    try {
      const response = await axios.get(`/wiki/w/api.php?action=query&list=search&srsearch=${searchText.value}&format=json`);

      listArticles.value = response.data;


      // if(listArticles.value.query.search.length === 0) {
      //   errorMessage.value = "Нет результатов";
      // }
      
      objArticles.value = listArticles.value.query.search
      console.log(objArticles);

    } catch (error) {
      console.error('Ошибка при выполнении запроса:', error);
    }
  }


  loading.value = false;

}


</script>






<style scoped>
  .wrapper{
    display: flex;
    max-width: 1280px;
    margin: 0 auto;
    font-weight: normal;
    min-height: 100vh;

  }

  .container{
    flex-grow: 1;
    margin-top: 30px;
    box-shadow: 0 4px 15px rgb(0 0 0 / 10%);
    background-color: white;
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    align-items: center;

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

  .error-message{
    margin-top: 30px;
    font-size: 20px;
  }

  .spinner{
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }



  @media (max-width: 330px) {
    .search-box{
      flex-direction: column;
    }
    
  }

  
  

  


</style>
