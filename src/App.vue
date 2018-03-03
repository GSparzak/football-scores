<template lang="html">
    <div class="" id="app">
        <h1>Football Scores</h1>
        <hr>
        {{ team }}
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            team: {}
        }
    },
    methods: {
        // getData() {
        //     fetch(`http://api.football-data.org/v1/teams/66`, {method: 'GET', mode: 'no-cors'})
        //     .then(response => response.json())
        //     .then(function (json) {
        //         console.log(json);
        //     })
        //     }
        },
     created() {
         // this.getData()
         axios.get('http://api.football-data.org/v1/teams/66')
         .then(response => response.json())
         .then(function (json) {
             console.log(json);
         })
     }
}
</script>

<style lang="scss">
 body {
     background-color: darkred;
     text-align: center;

     h1 {
         color: #fff;
     }

 }
</style>
