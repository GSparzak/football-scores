<template lang="html">
    <div class="leaguePage">

        <div class="leagueStats">
            <div class="panel fixtures">
                <h3 class="leagueCaption">{{ league.caption }}</h3>
                <div class="fixtures-header">
                    <i class="material-icons" @click="matchdayToShow--">chevron_left</i>
                    <h4>Gameweek {{ matchdayToShow }}</h4>
                    <i class="material-icons" @click="matchdayToShow++">chevron_right</i>
                </div>
                <table>
                    <tbody>
                        <tr v-for="item in currMatchday" >
                            <td class="teamName"><a href="#">{{ item.homeTeamName }}</a></td>
                            <!-- <td class="teamCrest"><img :src="item.homeTeamCrest"  style="width: 30px;"></td> -->
                            <td>{{ item.result.goalsHomeTeam }}</td>
                            <td>:</td>
                            <td>{{ item.result.goalsAwayTeam }}</td>
                            <!-- <td class="teamCrest"><img :src="item.awayTeamCrest" style="width: 30px;"></td> -->
                            <td class="teamName"><a href="#">{{ item.awayTeamName }}</a></td>
                        </tr>
                    </tbody>
                </table>
            </div>
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

    </div>
</template>

<script>
export default {
    data() {
        return {
            league: {},
            fixtures: {},
            table: {},
            teams: {},
            apiKey: '47a85bce93964ce586e5178391549dd0',
            matchdayToShow: ''
        }
    },
    computed: {
        currMatchday() {
            let currMatchday = [];
            let fixtures = this.fixtures.fixtures;
            if (typeof fixtures == 'undefined') {
                return currMatchday;
            }
            for (let i = 0; i < fixtures.length; i++) {
                if(fixtures[i].matchday === this.matchdayToShow) {
                    currMatchday.push(fixtures[i]);
                }
            }
            return currMatchday;
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
        fetchLeagueFixtures() {
            fetch('http://api.football-data.org/v1/competitions/445/fixtures', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.fixtures = json)
        },
        fetchLeagueTable() {
            fetch('http://api.football-data.org/v1/competitions/445/leagueTable', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.table = json)
        }
    },
    created() {
        this.fetchLeague();
        this.fetchLeagueFixtures();
        this.fetchLeagueTable();
    }
}
</script>

<style lang="scss">

.leaguePage {
    padding: 20px 100px;

    h3 {
        margin-bottom: 60px;
    }

    .leagueStats {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;

        .fixtures {
            min-width: 920px;

            .fixtures-header {
                display: flex;
                justify-content: space-between;
                align-items: center;

                .material-icons {
                    cursor: pointer;
                }
            }
        }

        .league-table-short {
            width: 400px;

            td, th {
                padding: 5px 0;
            }
        }
    }
}

</style>
