<template>
    <div class="newslist">

    </div>
</template>


<script>
    export default {
        name: 'newslist',
        data () {
            return {
                //Holds all sources retrieved fromt the external news api
                sources: [],
                //Holds the news source chosen by the user
                source: '',
            }

        },

    }
</script>

<style scoped>

</style>