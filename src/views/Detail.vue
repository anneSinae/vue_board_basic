<template>
  <div class="detail">
    <h1>목록상세페이지</h1>
    <p>{{ article.id }}</p>
    <p>{{ article.userId }}</p>
    <p>{{ article.title }}</p>
    <p>{{ article.body }}</p>

    <el-button @click="goBack">Back</el-button>
  </div>
</template>

<script>
import apiBoard from '@/api/board'

export default {
  name: 'Detail-sub',

  data() {
    return {
      article: "",
    }
  },
  
  mounted() {
    apiBoard.getArticle(this.$route.params.id)
    .then((response) => {
      this.article = response.data;
    })
    .catch((e) => {
          console.log(e);
    });
  },

  methods: {
    goBack() {
      this.$router.go(-1);
    }
  }
}
</script>