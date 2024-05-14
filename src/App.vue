<template>
  <div class="wrapper">

    <div class="container">
        <div class="search-box">
            <input class="search-input" type="text" placeholder="Введите запрос">
            <button class="search-button">Поиск</button>
        </div>

        <WikiItem :title="title" :content="content" :date="date" :link="link"/>
    </div>

  </div>
</template>



<script setup>


import { ref } from "vue";

import WikiItem from "./components/WikiItem.vue";

const title = "Заголовок статьи"
const content = "Подзаголовок статьи"
const date = "15.04.32"
const link = "ffff"


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
  }

  

  


</style>
