<template lang="html">
    <div class="leaguePage">
        <app-fixtures :leagueName="this.league.caption" :matchday="this.matchdayToShow" @showPreviousMatchday="matchdayToShow--" @showNextMatchday="matchdayToShow++"></app-fixtures>
        <div class="panel league-table-short">
            <table>
                <thead>
                    <tr>
                        <th>Pos.</th>
                        <th>Team</th>
                        <th>PTS</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="pos in table.standing">
                        <td>{{ pos.position }}</td>
                        <td><a href="#">{{ pos.teamName }}</a></td>
                        <td>{{ pos.points }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import Fixtures from './LeagueFixtures.vue'

export default {
    data() {
        return {
            league: {},
            table: {},
            teams: {},
            apiKey: '47a85bce93964ce586e5178391549dd0',
            matchdayToShow: ''
        }
    },
    methods: {
        fetchLeague() {
            fetch('http://api.football-data.org/v1/competitions/445', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => {
                this.league = json;
                this.matchdayToShow = json.currentMatchday;
            })
        },
        fetchLeagueTable() {
            fetch('http://api.football-data.org/v1/competitions/445/leagueTable', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.table = json)
        }
    },
    components: {
        appFixtures: Fixtures
    },
    created() {
        this.fetchLeague();
        this.fetchLeagueTable();
    }
}
</script>

<style lang="scss">

.leaguePage {
    padding: 20px 100px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;

    h3 {
        margin-bottom: 60px;
    }

    .league-table-short {
        width: 320px;

        td, th {
            padding: 5px 0;


                font-size: 14px;

        }
    }
}

</style>
