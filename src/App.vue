<template>
  <v-app>
    <v-card>
      <v-tabs v-model="selectedTeam" background-color="primary" dark>
        <v-tab v-for="team in teams" :key="team.name">
          {{ team.name }}
        </v-tab>
      </v-tabs>
      <v-tabs-items v-model="selectedTeam">
        <v-tab-item v-for="team in teams" :key="team.name">
          <team-table :players="team.players"></team-table>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import TeamTable from './components/TeamTable.vue';

export default {
  components: {
    TeamTable,
  },
  data() {
    return {
      selectedTeam: '',
      tab: null,
      teams: [
        {
          name: 'Houston Colt .45s',
          players: [
            {
              name: '',
              position: 'C',
              salary: 0,
            },
            {
              name: '',
              position: '1B',
              salary: 0,
            },
            {
              name: '',
              position: '2B',
              salary: 0,
            },
            {
              name: '',
              position: '3B',
              salary: 0,
            },
            {
              name: '',
              position: 'SS',
              salary: 0,
            },
            {
              name: '',
              position: 'OF1',
              salary: 0,
            },
            {
              name: '',
              position: 'OF2',
              salary: 0,
            },
            {
              name: '',
              position: 'OF3',
              salary: 0,
            },
            {
              name: '',
              position: 'Util',
              salary: 0,
            },
            {
              name: '',
              position: 'SP1',
              salary: 0,
            },
            {
              name: '',
              position: 'SP2',
              salary: 0,
            },
            {
              name: '',
              position: 'RP1',
              salary: 0,
            },
            {
              name: '',
              position: 'RP2',
              salary: 0,
            },
            {
              name: '',
              position: 'P1',
              salary: 0,
            },
            {
              name: '',
              position: 'P2',
              salary: 0,
            },
            {
              name: '',
              position: 'P3',
              salary: 0,
            },
            {
              name: '',
              position: 'B1',
              salary: 0,
            },
            {
              name: '',
              position: 'B2',
              salary: 0,
            },
            {
              name: '',
              position: 'B3',
              salary: 0,
            },
            {
              name: '',
              position: 'B4',
              salary: 0,
            },
            {
              name: '',
              position: 'B5',
              salary: 0,
            },
          ],
        },
        {
          name: 'Brooklyn Dodgers',
          players: [
            {
              name: 'Salvador Perez',
              position: 'C',
              salary: 45,
            },
            {
              name: 'Freddie Freeman',
              position: '1B',
              salary: 75,
            },
            {
              name: 'Ozzie Albies',
              position: '2B',
              salary: 40,
            },
            {
              name: 'Rafael Devers',
              position: '3B',
              salary: 46,
            },
            {
              name: 'Javier Baez',
              position: 'SS',
              salary: 31,
            },
            {
              name: 'Starling Marte',
              position: 'OF1',
              salary: 35,
            },
            {
              name: 'George Springer',
              position: 'OF2',
              salary: 32,
            },
            {
              name: 'Kyle Tucker',
              position: 'OF3',
              salary: 5,
            },
            {
              name: 'Eddie Rosario',
              position: 'Util',
              salary: 23,
            },
            {
              name: 'Aaron Nola',
              position: 'SP1',
              salary: 165,
            },
            {
              name: 'Jack Flaherty',
              position: 'SP2',
              salary: 165,
            },
            {
              name: 'Raisel Iglesias',
              position: 'RP1',
              salary: 93,
            },
            {
              name: 'Kirby Yates',
              position: 'RP2',
              salary: 57,
            },
            {
              name: 'Brandon Woodruff',
              position: 'P1',
              salary: 165,
            },
            {
              name: 'Zac Gallen',
              position: 'P2',
              salary: 190,
            },
            {
              name: 'Ryan Pressly',
              position: 'P3',
              salary: 69,
            },
            {
              name: 'Tyler Mahle',
              position: 'B1',
              salary: 54,
            },
            {
              name: 'Brady Singer',
              position: 'B2',
              salary: 14,
            },
            {
              name: 'Elieser Hernandez',
              position: 'B3',
              salary: 30,
            },
            {
              name: 'Adley Rutschman',
              position: 'B4',
              salary: 0,
            },
            {
              name: 'Joakim Soria',
              position: 'B5',
              salary: 3,
            },
          ],
        },
        { name: 'Detroit Stars', roster: ' name 1 roster' },
        { name: 'Zulu Cannibal Giants', roster: ' name 2 roster' },
        { name: 'Boston Braves', roster: ' name 3 roster' },
        { name: 'St. Louis Terriers', roster: ' name 4 roster' },
        { name: 'Seattle Pilots', roster: ' name 5 roster' },
        { name: 'Montreal Expos', roster: ' name 6 roster' },
        { name: 'Chicago Brownbombers', roster: ' name 7 roster' },
        { name: 'Washington Senators', roster: ' name 8 roster' },
        { name: 'California Angels', roster: ' name 9 roster' },
        { name: 'Atlanta BlackCrackers', roster: 'Tab 10 roster' },
      ],
    };
  },
  name: 'App',
};
</script>
