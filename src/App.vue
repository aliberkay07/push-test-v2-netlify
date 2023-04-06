<template>
  <!DOCTYPE html>
  <html lang="en">

  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css"
      integrity="sha512-HK5fgLBL+xu6dm/Ii3z4xhlSUyZgTT9tuc/hSrtw6uzJOvgRr2a9jyxxT1ely+B+xFAmJKVSTbpM/CuL7qxO8w=="
      crossorigin="anonymous" />
   
  </head>

  <body>
    <header>Push Notification | Web Push Nasıl Yapılır? | kablosuzkedi</header>
    <div class="app">
      <div class="categories">

        <category-item :category="category" v-for="category in categoryList" :key="category.id" />

      </div>
    </div>
  </body>

  </html>
</template>

<script>
import axios from "axios";
import CategoryItem from "./components/CategoryItem.vue"
export default {
  components: {
    CategoryItem,
  },
  data() {
    return {
      categoryList: [],
    }
  },
  created() {
    axios.get("https://push-test-v1.herokuapp.com/").then(categoryList_response => {
      console.log('categoryList :>> ', categoryList_response);
      this.categoryList = categoryList_response.data.categoryList;

    })
  }
}
</script>
