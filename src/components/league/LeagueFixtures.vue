<template lang="html">
    <div class="panel fixtures">
        <h3 class="leagueCaption">{{ leagueName }}</h3>
        <div class="fixtures-header">
            <i class="material-icons" @click="previousMatchday">chevron_left</i>
            <h4>Gameweek {{ matchday }}</h4>
            <i class="material-icons" @click="nextMatchday">chevron_right</i>
        </div>
        <table>
            <tbody>
                <tr v-for="item in currMatchday" >
                    <td class="teamName"><a href="#">{{ item.homeTeamName }}</a></td>
                    <!-- <td class="teamCrest"><img :src="item.homeTeamCrest"  style="width: 30px;"></td> -->
                    <td class="goals">{{ item.result.goalsHomeTeam }}</td>
                    <td>:</td>
                    <td class="goals">{{ item.result.goalsAwayTeam }}</td>
                    <!-- <td class="teamCrest"><img :src="item.awayTeamCrest" style="width: 30px;"></td> -->
                    <td class="teamName"><a href="#">{{ item.awayTeamName }}</a></td>
                </tr>
            </tbody>
        </table>
        <div class="button-wrapper">
            <a href="#" class="btn btn-danger">SHOW FULL TABLE</a>
        </div>

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
    props: ['leagueName', 'matchday'],
    computed: {
        currMatchday() {
            let currMatchday = [];
            let fixtures = this.fixtures.fixtures;
            if (typeof fixtures == 'undefined') {
                return currMatchday;
            }
            for (let i = 0; i < fixtures.length; i++) {
                if(fixtures[i].matchday === this.matchday) {
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
        },
        previousMatchday() {
            this.$emit('showPreviousMatchday');
        },
        nextMatchday() {
            this.$emit('showNextMatchday');
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

        table {

            tr:hover {
                background-color: #777;
            }

            td {
                line-height: 30px;
            }

            .teamName {
                width: 40%;
            }

            .goals {
                font-weight: 700;
                font-size: 20px;
            }
        }

        .button-wrapper {
            margin: 30px 0 0;
            text-align: right;
        }
    }
</style>
