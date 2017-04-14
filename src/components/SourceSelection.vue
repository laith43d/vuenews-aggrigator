<template>
    <div class="sourceselection">
        <h4>Please select news source:</h4>
        <select class="form-control" @change="sourceChanged">
            <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
        </select>
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
                for (let i=0; i<this.sources.length; i++)
                {
                    if (this.sources[i].id == e.target.value)
                    {
                        this.source = this.sources[i]
                    }
                }
            }
        },
        created: function () {
            this.$http.get('https://newsapi.org/v1/sources?language=en')
                .then(response => {
                    this.sources = response.data.sources;
                })
        }

    }
</script>

<style scoped>

</style>