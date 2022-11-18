<template>
  <div class="top">
    <transition name="moveInUp">
    <div :class="{left:isShow}" v-if="isShow">
      <article class="wrapper-2017">
        <b-container>
          <BoardView :article="article"></BoardView>
        </b-container>
      </article>
    </div>
    </transition>
    <div :class="{right:isShow, center:!isShow}" id="right">
      <article class="wrapper-2017">
        <b-container class="bv-example-row mt-3">
          <b-col>
            <b-row class="mb-1">
              <b-col class="text-right">
                <b-button variant="outline-primary" @click="moveWrite()"
                  >글쓰기</b-button
                >
              </b-col>
            </b-row>
  
            <b-row>
              <b-col>
                <!-- <b-container v-if="articles && articles.length != 0" class="bv-example-row mt-3">
                    <board-list-item v-for="(article, index) in articles" :key="index" :article="article"></board-list-item>
                </b-container> -->
                <b-table
                  id="my-table"
                  hover
                  :items = "articles"
                  :fields="fields"
                  @row-clicked="viewArticle"
                  :per-page="perPage"
                  :current-page="currentPage"
                >
                <template #cell(subject)="data">
                    {{ data.item.subject }}
                </template>
                </b-table>
                
                <b-pagination
                  v-model="currentPage"
                  pills
                  :total-rows="rows"
                  :per-page="perPage"
                  aria-controls="my-table"
                  align="center"
                  size="sm"
                ></b-pagination>
              </b-col>
            </b-row>
          </b-col>
        </b-container>
      </article>
    </div>
  </div>
</template>

<script>
import http from "@/api/http";
import BoardView from "./BoardView.vue";
import BoardListItem from "@/components/board/item/BoardListItem";
export default {
    name: "BoardList",
    data() {
        return {
            isShow: false,
            perPage: 10,
            currentPage: 1,
            articles: [],
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
            this.articles = data;
        });
    },
    computed: {
        rows() {
            return this.articles.length;
        },
    },
    methods: {
        moveWrite() {
            this.$router.push({ name: "boardwrite" });
        },
        viewArticle(article) {
            this.isShow = true;
            this.article=article;
        },
    },
    components: {
       BoardView,
       BoardListItem,
    },
};
</script>

<style scope>

.moveInUp-enter-active{
  opacity: 0;
  transition: opacity 1s ease-in;
}
.moveInUp-enter-active{
  animation: fadeIn 1s ease-in;
}
@keyframes fadeIn{
  0%{
    opacity: 0;
  }
  50%{
    opacity: 0.5;
  }
  100%{
    opacity: 1;
  }
}
.info span,
span.about-the-item {
  display: block;
  font-size: 12px;
  margin-bottom: 5px;
  color: rgba(0, 0, 0, 0.4);
  margin-top: 43px;
}

.info {
  clear: none;
}

ul.article-list {
  margin-left: 30px;
  list-style-type: none;
}

.wrapper-2017{
  background-color: white;
}
article.wrapper-2017 p {
  padding-right: 8px;
  margin-top: -5px;
}

ul.article-list li::before {
  content: "-";
  display: block;
  float: left;
  margin-right: 5px;
}

.info-box a {
  color: #1488cc;
  text-decoration: none;
}

article.wrapper-2017 .accent {
  font-family: monospace;
  display: inline-block;
  width: 25%;
  color: rgba(0, 0, 0, 0.5);
  font-size: 11px;
}

article.wrapper-2017 p + p {
  color: rgb(51, 51, 51);
  margin-bottom: 0;
}

.box-content > div.container {
  width: auto;
  margin-top: 20px;
}

main article video {
  width: 100%;
}

main figure img {
  z-index: 99;
  width: 100%;
}

main figure img + img {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -999;
}

main figure:hover img + img {
  z-index: 1;
}

main .img-extra::after {
  display: block;
  padding: 0 10px;
  content: "hover to play";
  position: absolute;
  left: -25px;
  top: 150px;
  font-size: 14px;
  color: #ffeaa7;
  text-align: center;
  background: #1f2029;
  transform-origin: 0 0;
  transform: rotate(270deg);
  transition: 0.1s ease-in-out;
  z-index: -1;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

main figure .img-extra::after {
  left: -50px;
}

main video:hover + .img-extra::after,
main img:hover + .img-extra::after {
  left: 0;
  box-shadow: none;
}

.sitemap {
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto;
  grid-gap: 20px;
}

.sitemap .card {
  min-height: 100%;
  background: white;
  box-shadow: 13px 32px 36px -14px hsla(0, 0%, 70%, 0.1);
  display: flex;
  flex-direction: column;
  text-decoration: none;
  color: #444;
  position: relative;
  top: 0;
  transition: all 0.1s ease-in;
}

.sitemap .card:hover {
  top: -2px;
  box-shadow: 13px 32px 36px -14px hsla(0, 0%, 70%, 0.3);
}

.sitemap .card article {
  padding: 20px;
  display: flex;
  flex: 1;
  justify-content: space-between;
  flex-direction: column;
}

.sitemap h3 {
  font-size: 14px;
  line-height: 16px;
  margin: 0;
  color: #333;
}

.sitemap .card span {
  font-size: 10px;
  color: #999;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin: 2em 0 0 0;
}

@media only screen and (min-width: 476px) {
  .sitemap {
    grid-template-columns: 1fr 1fr;
  }
}

@media only screen and (min-width: 960px) {
  .sitemap {
    grid-template-columns: 1fr 1fr 1fr;
  }
  .sitemap-item-feature {
    grid-column: 1 / span 2;
  }
}

@media only screen and (min-width: 1296px) {
  .sitemap {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

div.link {
  margin-bottom: 50px;
}

@media (max-width: 768px) {
  article.wrapper-2017 {
    font-size: 14.4px;
  }
  .info-box .info {
    width: 100%;
    text-align: center;
  }
  .info-box .info h4 {
    margin-top: 10px;
  }
  article.wrapper-2017 .accent {
    display: block;
    width: 100%;
    margin-top: 10px;
    margin-bottom: 0;
  }
}

a.wrapper-news {
  display: block;
  margin-bottom: 50px;
  box-shadow: none;
}

a.wrapper-news:hover {
  box-shadow: none;
}

.wrapper-news article {
  padding-bottom: 5%;
}

.wrapper-news img {
  border: none;
}

.wrapper-news h3,
.wrapper-news p {
  padding: 0 5%;
  margin-bottom: 2%;
}

.wrapper-news p {
  font-size: 1rem;
}

.wrapper-news .date {
  padding: 0 5%;
  font-size: 0.8rem;
  font-family: monospace;
}

.wrapper-news:nth-child(odd) article {
  background: rgba(246, 244, 242, 0.5);
}

.wrapper-news:nth-child(odd) article .date {
  color: rgb(183, 181, 179);
}

.wrapper-news:nth-child(even) article {
  background: #1d1e22;
  color: rgb(246, 244, 242);
}

.wrapper-news:nth-child(even) article h3 {
  color: rgb(246, 244, 242);
}

.wrapper-news:nth-child(even) article .date {
  color: rgb(183, 181, 179);
}

div.wrapper {
  display: flex;
  flex-direction: row-reverse;
  max-width: calc(var(--nav-width) + var(--gap) * 2);
  margin: 0 auto;
}

aside {
  height: 100% !important;
  margin-top: 48px;
  padding-left: 10px;
  width: 25%;
  margin-left: var(--gap);
  border-radius: 8px;
  border-color: #f9f9f9;
  background-color: #f9f9f9;
}

.main {
  width: 75%;
  margin-right: 0;
}

@media (max-width: 960px) {
  div.ads,
  div.navi ul span {
    display: none;
  }
  div.wrapper {
    display: block;
  }

  .main {
    width: 100%;
    margin-right: auto;
  }
  aside {
    position: relative;
    width: 90%;
    margin-left: var(--gap);
    margin-right: var(--gap);
    margin-bottom: 50px;
  }

  div.navi ul li {
    display: inline-block;
    width: 24%;
  }
}

@media (max-width: 478px) {
  div.navi ul li {
    width: 49%;
  }
}

.ads-header {
  max-width: calc(var(--nav-width) + var(--gap) * 2);
  margin: 20px auto;
}

.ads {
  margin-bottom: 50px;
}
div.navi {
  margin-bottom: 50px;
  padding: 15px 0 0 25px;
}

div.navi h4 {
  margin-bottom: 5px;
  font-size: 10px;
  color: #555;
  text-transform: uppercase;
}

div.navi ul li {
  font-size: 16px;
  list-style-type: none;
}

div.navi ul li i {
  width: 25px;
  font-size: 16px;
}

div.navi ul li i.custom {
  display: inline-block;
  font-weight: bold;
  font-size: 12px;
}

div.navi ul li a {
  transition: 0.2s ease-in-out;
}

div.navi ul li a.html-menu:hover {
  color: #e54d26;
}

div.navi ul li a.css-menu:hover {
  color: #006fb9;
}

div.navi ul li a.bs-menu:hover {
  color: #6d15ed;
}

div.navi ul li a.js-menu:hover {
  color: #cfb432;
}

div.navi ul li a.jq-menu:hover {
  color: #1b75bb;
}

div.navi ul li a.react-menu:hover {
  color: #61dafb;
}

div.navi ul li a.vue-menu:hover {
  color: #4dba87;
}

div.navi ul li a.books-menu:hover {
  color: #f3797a;
}

div.navi ul li a.speed-code-menu:hover {
  color: #486b4e;
}

span.badge {
  margin-left: 15px;
  color: #1488cc;
}

article.digest {
  margin: 120px 0;
}

.gsib_a,
.gsc-search-button {
  line-height: 1;
}

#___gcse_0 {
  width: 100%;
  padding: 0;
}

.post-entry {
  padding-bottom: 50px;
  transition: 0.2s ease-in-out;
  box-shadow: 0 0 0 1px rgba(53, 72, 91, 0.07), 0 2px 2px rgba(0, 0, 0, 0.01),
    0 4px 4px rgba(0, 0, 0, 0.02), 0 10px 8px rgba(0, 0, 0, 0.03),
    0 15px 15px rgba(0, 0, 0, 0.03), 0 30px 30px rgba(0, 0, 0, 0.04),
    0 70px 65px rgba(0, 0, 0, 0.05);
}

.post-entry:hover {
  box-shadow: 0 0 0 1px rgba(53, 72, 91, 0.04), 0 2px 2px rgba(0, 0, 0, 0),
    0 4px 4px rgba(0, 0, 0, 0.01), 0 10px 8px rgba(0, 0, 0, 0.02),
    0 15px 15px rgba(0, 0, 0, 0.02), 0 30px 30px rgba(0, 0, 0, 0.02),
    0 70px 65px rgba(0, 0, 0, 0.03);
}

h2.subheader {
  margin-top: 150px;
}

.tailwind {
  display: inline-block;
  width: 12px;
  height: 12px;
  background: no-repeat
    url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 54 33'%3E%3Cg clip-path='url(%23prefix__clip0)'%3E%3Cpath fill='%2338bdf8' fill-rule='evenodd' d='M27 0c-7.2 0-11.7 3.6-13.5 10.8 2.7-3.6 5.85-4.95 9.45-4.05 2.054.513 3.522 2.004 5.147 3.653C30.744 13.09 33.808 16.2 40.5 16.2c7.2 0 11.7-3.6 13.5-10.8-2.7 3.6-5.85 4.95-9.45 4.05-2.054-.513-3.522-2.004-5.147-3.653C36.756 3.11 33.692 0 27 0zM13.5 16.2C6.3 16.2 1.8 19.8 0 27c2.7-3.6 5.85-4.95 9.45-4.05 2.054.514 3.522 2.004 5.147 3.653C17.244 29.29 20.308 32.4 27 32.4c7.2 0 11.7-3.6 13.5-10.8-2.7 3.6-5.85 4.95-9.45 4.05-2.054-.513-3.522-2.004-5.147-3.653C23.256 19.31 20.192 16.2 13.5 16.2z' clip-rule='evenodd'/%3E%3C/g%3E%3Cdefs%3E%3CclipPath id='prefix__clip0'%3E%3Cpath fill='%23fff' d='M0 0h54v32.4H0z'/%3E%3C/clipPath%3E%3C/defs%3E%3C/svg%3E");
  filter: brightness(0%);
  transition: 0.2s ease-in-out;
}

a.tailwind-menu:hover {
  color: #38bdf8;
}

a.tailwind-menu:hover .tailwind {
  filter: brightness(100%);
}

.adsbygoogle {
  box-shadow: 0 0 0 1px rgba(53, 72, 91, 0.04), 0 2px 2px rgba(0, 0, 0, 0),
    0 4px 4px rgba(0, 0, 0, 0.01), 0 10px 8px rgba(0, 0, 0, 0.02),
    0 15px 15px rgba(0, 0, 0, 0.02), 0 30px 30px rgba(0, 0, 0, 0.02),
    0 70px 65px rgba(0, 0, 0, 0.03);
}



.bv-example-row{
  margin-top: 200px;
}

div.left{
  float: left;
  width: 50%;
  background-color: white;
}

div.right{
  float: right;
  width: 50%;
  background-color: white;
}

.top{
  background-color: 111111;
  height: 100%;
}
div.center{
  float: center;
  width: 50%;
  margin-left: calc(24.5%);  
  background-color: white;
}
</style>
