<template>
  <b-container class="bv-example-row mt-3">
    <article class="wrapper-2017">
      <b-img
        :src="require('@/assets/별이빛나는밤.png')"
        id="logo"
        alt="logo"
      ></b-img>
      <div class="img-extra"></div>
      <div class="info-box">
        <div class="info info-author">
          <h4>Author</h4>
          <li>{{ article.userid }}</li>
        </div>
        <div class="info info-author">
          <h4>RegistTime</h4>
          <li>
            <time>{{ article.regtime }}</time>
          </li>
        </div>
        <div class="info info-link">
          <h4>Links</h4>
          <ul>
            <li>
              <a href="https://codepen.io/ahmadbassamemran/pen/rNjMXqg" target="_blank"
                >demo and code</a
              >
            </li>
          </ul>
        </div>
      </div>
      <h4 class="about-the-item">subject</h4>
      <b-card-body class="text-center">
        <div>{{ article.subject }}</div>
      </b-card-body>
      <h4 class="about-the-item">content</h4>
      <b-card-body class="text-center">
        <div v-html="message"></div>
      </b-card-body>
      <b-col class="text-right">
        <b-button variant="outline-info" size="sm" @click="moveModifyArticle" class="mr-2"
          >글수정</b-button
        >
        <b-button variant="outline-danger" size="sm" @click="deleteArticle">글삭제</b-button>
      </b-col>
    </article>
    <!-- <b-row>
      <b-col>
        <b-alert show><h3>글보기</h3></b-alert>
      </b-col>
    </b-row> -->
    <!-- <b-row class="mb-1">
      <b-col class="text-left">
        <b-button variant="outline-primary" @click="moveList">목록</b-button>
      </b-col>
    </b-row> -->
  </b-container>
</template>

<script>
// import moment from "moment";
import http from "@/api/http";

export default {
  name: "BoardDetail",
  data() {
    return {
      article: {},
    };
  },

  props:{
    article: Object,
  },
  computed: {
    message() {
      if (this.article.content) return this.article.content.split("\n").join("<br>");
      return "";
    },
  },
  created() {
    http.get(`/board/${this.$route.params.articleno}`).then(({ data }) => {
      this.article = data;
    });
  },
  methods: {
    moveModifyArticle() {
      this.$router.replace({
        name: "boardmodify",
        params: { articleno: this.article.articleno },
      });
      //   this.$router.push({ path: `/board/modify/${this.article.articleno}` });
    },
    deleteArticle() {
      if (confirm("정말로 삭제?")) {
        this.$router.replace({
          name: "boarddelete",
          params: { articleno: this.article.articleno },
        });
      }
    },
    moveList() {
      this.$router.push({ name: "boardlist" });
    },
  },
  // filters: {
  //   dateFormat(regtime) {
  //     return moment(new Date(regtime)).format("YY.MM.DD hh:mm:ss");
  //   },
  // },
};
</script>

<style>
article.wrapper-2017 {
  position: relative;
  transition: 0.3s ease-in-out;
  font-size: 16px;
  margin-top: 100px;
  margin-bottom: 100px;
  padding: var(--gap);
  background: var(--entry);
  border-radius: 8px;
  box-shadow: 0 0 0 1px rgba(53, 72, 91, 0.07), 0 2px 2px rgba(0, 0, 0, 0.01),
    0 4px 4px rgba(0, 0, 0, 0.02), 0 10px 8px rgba(0, 0, 0, 0.03), 0 15px 15px rgba(0, 0, 0, 0.03),
    0 30px 30px rgba(0, 0, 0, 0.04), 0 70px 65px rgba(0, 0, 0, 0.05);
}

article.wrapper-2017:hover {
  box-shadow: 0 0 0 1px rgba(53, 72, 91, 0.04), 0 2px 2px rgba(0, 0, 0, 0),
    0 4px 4px rgba(0, 0, 0, 0.01), 0 10px 8px rgba(0, 0, 0, 0.02), 0 15px 15px rgba(0, 0, 0, 0.02),
    0 30px 30px rgba(0, 0, 0, 0.02), 0 70px 65px rgba(0, 0, 0, 0.03);
}

.info-box .info {
  box-sizing: border-box;
  float: left;
  width: 33.3333333333%;
  padding: 0;
  min-height: 50px;
}

.info-box .info h4,
h4.about-the-item {
  font-size: 11px;
  line-height: 11px;
  margin-bottom: 9px;
  color: rgba(0, 0, 0, 0.5);
  margin-top: 33px;
  text-transform: none;
  font-weight: 400;
  font-family: monospace;
}

article.wrapper-2017 figure {
  position: relative;
  margin: 0;
}

article.wrapper-2017 h3 + p {
  margin-bottom: 33px;
}

.info-box {
  overflow: hidden;
}

.info-box .info ul {
  padding: 0;
  margin: 0;
  list-style: none;
}

article.wrapper-2017 h3 {
  margin: 10px 0 5px !important;
  font-size: 18px;
  text-transform: uppercase;
}

article.wrapper-2017::after {
  content: " ";
  display: block;
  padding: 20px;
  margin: 10px auto;
  width: 100%;
}
</style>
