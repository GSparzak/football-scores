<template lang="html">
    <div class="" id="app">
        <v-app dark>
            <v-container>
                <v-layout>
                    <v-flex class="text-xs-center"><h1>Football Scores</h1></v-flex>
                </v-layout>
                <v-layout flagSelect>
                    <v-flex md3 text-md-center>
                        <a href="#">
                            <img src="/images/england_football_icon_256.png" alt="">
                        </a>
                        <p>premier league</p>
                    </v-flex>
                    <v-flex md3 text-md-center>
                        <a href="#">
                            <img src="/images/france_football_icon_256.png" alt="">
                        </a>
                        <p>Ligue 1</p>
                    </v-flex>
                    <v-flex md3 text-md-center>
                        <a href="#">
                            <img src="/images/germany_football_icon_256.png" alt="">
                        </a>
                        <p>1 bundesliga</p>
                    </v-flex>
                    <v-flex md3 text-md-center>
                        <a href="#">
                            <img src="/images/netherlands_football_icon_256.png" alt="">
                        </a>
                        <p>eredivisie</p>
                    </v-flex>
                </v-layout>
                <v-layout>
                    <v-flex text-md-center my-3><h3>{{ league.caption }}</h3></v-flex>
                </v-layout>
                <v-layout elevation-4 wrap grey darken-3 my-5 px-2>
                    <v-flex md12>
                        <h4 md12 text-md-center>Gameweek {{ league.currentMatchday }}</h4>
                    </v-flex>
                    <v-flex md12 text-md-center>
                        <table>
                            <tbody>
                                <tr v-for="item in currMatchday">
                                    <td>{{ item.homeTeamName }}</td>
                                    <td><img :src="item.homeTeamCrest"  style="width: 30px;"></td>
                                    <td>{{ item.result.goalsHomeTeam }}</td>
                                    <td>:</td>
                                    <td>{{ item.result.goalsAwayTeam }}</td>
                                    <td><img :src="item.awayTeamCrest" style="width: 30px;"></td>
                                    <td>{{ item.awayTeamName }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </v-flex>
                </v-layout>
                <v-layout elevation-4 grey darken-3 my-5 px-2>
                    <v-flex md12>
                        <table>
                            <thead>
                                <tr>
                                    <th>Pos.</th>
                                    <th>Team</th>
                                    <th>GP</th>
                                    <th>GW</th>
                                    <th>GD</th>
                                    <th>GL</th>
                                    <th>GF</th>
                                    <th>GA</th>
                                    <th>GD</th>
                                    <th>PTS</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="pos in table.standing">
                                    <td>{{ pos.position }}</td>
                                    <td>{{ pos.teamName }}</td>
                                    <td>{{ pos.playedGames }}</td>
                                    <td>{{ pos.wins }}</td>
                                    <td>{{ pos.draws }}</td>
                                    <td>{{ pos.losses }}</td>
                                    <td>{{ pos.goals }}</td>
                                    <td>{{ pos.goalsAgainst }}</td>
                                    <td>{{ pos.goalDifference }}</td>
                                    <td>{{ pos.points }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </v-flex>
                </v-layout>
                <v-layout>
                    <v-flex md12>
                        <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-app>
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
            apiKey: '47a85bce93964ce586e5178391549dd0'
            // manUtd: {
            //     crest: 'https://upload.wikimedia.org/wikipedia/de/d/da/Manchester_United_FC.svg',
            //     name: 'Manchester United F.C.',
            //     estDate: 1982,
            //     stadium: 'Old Trafford',
            //     stadiumCapacity: 75000,
            //     squad: {
            //         goalkeepers: ['David de Gea', 'Sergio Romero', 'Joel Pereira', 'Sam Johnstone'],
            //         defenders: ['Chris Smalling', 'Phil Jones', 'Marcos Rojo', 'Antonio Valencia', 'Victor Lindelof', 'Eric Bailly', 'Luke Shaw', 'Daley Blind', 'Matteo Darmian'],
            //         midfielders: ['Paul Pogba', 'Juan Mata', 'Jesse Lingard', 'Ashley Young', 'Nemanja Matic', 'Michael Carrick', 'Scott McTomminay', 'Ander Herrera', ' Marouane Fellaini'],
            //         forwards: ['Romelu Lukaku', 'Zlatan Ibrahimovich', 'Alexis Sanchez', 'Anthony Martial', 'Marcus Rashford']
            //     }
            // }
        }
    },
    methods: {
        fetchLeague() {
            fetch('http://api.football-data.org/v1/competitions/445', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
            .then(response => response.json())
            .then(json => this.league = json)
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
        },
        // fetchLeagueTeams() {
        //     fetch('http://api.football-data.org/v1/competitions/445/teams', {method: 'GET', headers: {'X-Auth-Token': this.apiKey}})
        //     .then(response => response.json())
        //     .then(json => this.teams = json)
        // }

    },
    computed: {
        currMatchday() {
            let currMatchday = [];
            let fixtures = this.fixtures.fixtures;
            let apiKey = this.apiKey;
            if (typeof fixtures == 'undefined') {
                return currMatchday;
            }

            for (let i = 0; i < this.fixtures.fixtures.length; i++) {
                if(fixtures[i].matchday === this.league.currentMatchday) {
                    // let getHomeTeamCrest = new Promise(function(resolve, reject) {
                    //     return fetch(fixtures[i]._links.homeTeam.href, {method: 'GET', headers: {'X-Auth-Token': apiKey}})
                    //     .then(response => response.json())
                    //     .then(function(json) {
                    //         fixtures[i].homeTeamCrest = json.crestUrl;
                    //         console.log('homeTeamCrest');
                    //         resolve(fixtures[i]);
                    //     });
                    // });
                    // let getAwayTeamCrest = new Promise(function(resolve, reject) {
                    //     return fetch(fixtures[i]._links.awayTeam.href, {method: 'GET', headers: {'X-Auth-Token': apiKey}})
                    //     .then(response => response.json())
                    //     .then(function(json) {
                    //         fixtures[i].awayTeamCrest = json.crestUrl;
                    //         console.log('awayTeamCrest');
                    //         resolve(fixtures[i]);
                    //     });
                    // });
                    function getHomeTeamCrest (){
                        return new Promise(function(resolve, reject) {
                            fetch(fixtures[i]._links.homeTeam.href, {method: 'GET', headers: {'X-Auth-Token': apiKey}})
                        })
                        .then(response => response.json())
                        .then(function(json) {
                            fixtures[i].homeTeamCrest = json.crestUrl;
                            console.log('homeTeamCrest');
                            Promise.resolve(fixtures[i]);
                        });
                    };
                    function getAwayTeamCrest (){
                        return new Promise(function(resolve, reject) {
                            fetch(fixtures[i]._links.awayTeam.href, {method: 'GET', headers: {'X-Auth-Token': apiKey}})
                        })
                        .then(response => response.json())
                        .then(function(json) {
                            fixtures[i].awayTeamCrest = json.crestUrl;
                            console.log('awayTeamCrest');
                            Promise.resolve(fixtures[i]);
                        });
                    };
                    Promise.all([getHomeTeamCrest(), getAwayTeamCrest()])
                    .then(function (values) {
                        console.log(values);
                        currMatchday.push(fixtures[i]);
                        console.log(currMatchday);
                        return currMatchday;
                    })
                }
            }
        }
    },
    created() {
        this.fetchLeague();
        this.fetchLeagueFixtures();
        this.fetchLeagueTable();
        // this.fetchLeagueTeams();
    }
}
</script>

<style lang="scss">
* {
    font-family: 'Exo 2', 'Roboto', sans-serif;
}

h1 {
    font-family: 'Audiowide', cursive;
    text-transform: uppercase;
    letter-spacing: 3px;
    margin: 20px 0;
    font-size: 40px;
}

h3 {
    font-family: 'Audiowide', cursive;
    font-size: 24px;
}

h4 {
    width: 100%;
    text-align: center;
}

.flagSelect{
    .flex {
        a {
            display: block;

            img {
                width: 200px;
                height: auto;
            }
        }
        p {
            text-transform: uppercase;
        }
    }
}
table {
    width: 100%;
    border-bottom: 0 solid #777;
    border-collapse: collapse;

    tr {
        border-bottom: 1px solid #777;
        border-collapse: collapse;

        td, th {
            text-align: center;
            border-bottom: 1px solid #777;
            border-collapse: collapse;
            padding: 10px 0;
        }
    }

        tr:last-of-type,
        tr:last-of-type td {
            border-bottom: none !important;
        }

}

img{
    width: 100%;
}
li {
    list-style-type: none;
     color: #fff;
 }
</style>
