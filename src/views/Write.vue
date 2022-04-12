<template>
  <div class="write">
    <h1>글작성</h1>
    <el-input type="text" v-model="title"></el-input>
    <el-input type="textarea" rows="10" v-model="contents"></el-input>

    <el-button @click="writeArticle">저장</el-button>
    <el-button @click="goBack">Back</el-button>
  </div>
</template>

<script>
import apiBoard from '@/api/board'

export default {
  name: 'Write-sub',

  data() {
    return {
      title: "",
      contents: "",
    }
  },

  methods: {
    goBack() {
      this.$router.go(-1);
    },

    writeArticle() {
      if(!this.title || !this.contents) {
        this.$message.error("제목과 본문을 작성해주세요.");
        return;
      }

      apiBoard.postArticle(0, this.title, this.contents)
        .then((response) => {
          console.log(response);
          this.$router.push({path: "/"});
        })
        .catch((e) => {
              console.log(e);
              this.$message.error("게시물 작성 중 에러가 발생했습니다.")
        });
        
    }
  }
}
</script>