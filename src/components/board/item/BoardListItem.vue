<template>
  <b-tr>
    <b-td>{{ article.subject }}</b-td>
    <b-td>{{ article.userid }}</b-td>
    <b-td>{{ article.regtime }}</b-td>
    <b-td>{{ article.hit }}</b-td>
  </b-tr>
</template>

<script>
export default {
  name: "BoardListItem",
  props: {
    article: Object,
  },
  data() {
    return {
      fields: [
        { key: "file", label: "", tdClass: "tdClass" },
        // { key: "articleno", label: "글번호", tdClass: "tdClass" },
        { key: "subject", label: "제목", tdClass: "tdSubject" },
        { key: "userid", label: "작성자", tdClass: "tdClass" },
        { key: "regtime", label: "작성일", tdClass: "tdClass" },
        { key: "hit", label: "조회수", tdClass: "tdClass" },
      ],
      article: {},
    };
  },
  created() {
    http.get(`/board`).then(({ data }) => {
      this.article = data;
    });
  },
};
</script>

<style></style>
