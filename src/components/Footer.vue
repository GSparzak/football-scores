<template lang="html">
    <footer>
        <a href="#" v-for="team in teams.teams" :title="team.name" :style="{'backgroundImage': 'url(' + team.crestUrl + ')'}"></a>
    </footer>
</template>

<script>
export default {
    data() {
        return {
            teams: {},
            apiKey: '47a85bce93964ce586e5178391549dd0'
        }
    },
    methods: {
        fetchLeagueTeams() {
            fetch('http://api.football-data.org/v1/competitions/445/teams', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.teams = json)
        }
    },
    created() {
        this.fetchLeagueTeams();
    }
}
</script>

<style lang="scss">
    footer {
        width: 100%;
        display: flex;
        justify-content: space-around;
        position: fixed;
        bottom: 0;
        left: 0;
        padding: 10px 40px;
        background-color: #eee;

        a {
            width: 40px;
            height: 40px;
            display: inline-block;
            position: relative;
            background: center center/contain no-repeat;

            &:before {
                content: '';
                padding-bottom: 100%;
                position: absolute;
                top: 0;
                left: 0;
            }
        }
    }
</style>
