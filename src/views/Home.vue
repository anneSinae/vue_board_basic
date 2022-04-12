<template>
  <h1>Hello Anne</h1>
</template>

<script>
import apiBoard from "@/api/board";
export default {
  name: 'Home-main',
  mounted() {
    apiBoard.getArticle(1)
      .then((response) => {
          console.log("getArticle", response);
          this.articles = response.data;
      })
      .catch((e) => {
          console.log(e);
      });

    
    apiBoard.getArticles(0)
      .then((response) => {
          console.log("getArticles", response);
          this.articles = response.data;
      })
      .catch((e) => {
          console.log(e);
      });

    apiBoard.postArticle("userId", "title", "body")
      .then(function (response) {
        console.log("postArticle", response);
      })
      .catch(function (e) {
        console.log(e);
      });
      
  },
}
</script>
