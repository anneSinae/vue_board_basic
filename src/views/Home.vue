<template>
  <h1>{{title}}</h1>

  <el-table @row-click="rowClicked" :data="articles" style="width: 100%">
    <el-table-column prop="id" label="id" width="80">
    </el-table-column>
    <el-table-column prop="userId" label="userId" width="120">
    </el-table-column>
    <el-table-column prop="title" label="title"> </el-table-column>
  </el-table>

  <br>
  <a href="/board/write" class="btn-write">글쓰기</a>
</template>

<script>
import apiBoard from "@/api/board";
export default {
  name: 'Home-main',

  data() {
    return {
      title: "Hello Anne",
      articles: null,
    }
  },

  mounted() {
    apiBoard.getArticles(0)
      .then((response) => {
          console.log("getArticles", response);
          this.articles = response.data;
      })
      .catch((e) => {
          console.log(e);
      });

  },

  methods: {
    rowClicked(row) {
      this.$router.push({
        path: `/board/detail/${row.id}`
      });
    }
  }
}
</script>

<style scoped>
.btn-write {position: fixed; right: 20px; bottom: 20px;}
</style>
