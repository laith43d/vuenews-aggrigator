<template>
  <div class="newslist">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" v-bind:src="article.urlToImage">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
            </h4>
            <h5 v-if="article.author"><i>by {{article.author}}</i></h5>
            <p>{{article.description}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
  export default {
    name: 'newslist',
    data () {
      return {
        articles: [],
      }
    },
    props: ['source'],
    watch: {
      source: function (val) {
        this.updateSource(val)
      }
    },
//        created: function () {
//            this.updateSource(this.source)
//        },
    methods: {
      updateSource: function (source) {
        this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=917b585fa2da4c23b15e171a43bbdf18')
          .then(response => {
            this.articles = response.data.articles;
          })
      }
    }

  }
</script>

<style scoped>
  .media-object {
    width: 128px;
    padding: 10px;
  }

  .media {
    border-top: 1px solid lightgrey;
    padding-top: 10px;
  }
</style>
