<template lang="html">
    <div class="panel fixtures">
        <h3 class="leagueCaption">{{ leagueName }}</h3>
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
</template>

<script>
export default {
    data() {
        return {
            fixtures: {},
            apiKey: '47a85bce93964ce586e5178391549dd0',
            matchdayToShow: ''
        }
    },
    props: ['leagueName'],
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
        fetchLeagueFixtures() {
            fetch('http://api.football-data.org/v1/competitions/445/fixtures', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.fixtures = json)
        }
    },
    created() {
        this.fetchLeagueFixtures();
    }
}
</script>

<style lang="scss">
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
</style>
