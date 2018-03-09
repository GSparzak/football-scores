<template lang="html">
    <div class="panel league-table-full">
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
    </div>
</template>

<script>
export default {
}
</script>

<style lang="css">
</style>
