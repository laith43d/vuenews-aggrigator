<template>
  <div class="sourceselection">
    <div class="jumbotron">
      <h2><span class="glyphicon glyphicon-list-alt"></span> News Sources Selector</h2>
      <h4>Please select news source:</h4>
      <select class="form-control" @change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
      </select>
      <div v-if="source">
        <h6>{{source.description}}</h6>
        <a v-bind:href="source.url" class="btn btn-primary" target="_blank">go to {{source.name}} website</a>
      </div>
    </div>
  </div>
</template>


<script>
  export default {
    name: 'sourceselection',
    data () {
      return {
        //Holds all sources retrieved from the external news api
        sources: [],
        //Holds the news source chosen by the user
        source: '',
      }

    },
    methods: {
      sourceChanged: function (e) {
        for (let i = 0; i < this.sources.length; i++) {
          if (this.sources[i].id === e.target.value) {
            this.source = this.sources[i]
          }
        }
        this.$emit('sourceChanged', e.target.value)
      }
    },
    created: function () {
      this.$http.get('https://newsapi.org/v1/sources?language=en')
        .then(response => {
          this.sources = response.data.sources;
          this.source = this.sources[0]
        })
    }

  }
</script>

<style scoped>

</style>
