<template>
  <v-app>
    <v-tabs vertical dark background-color="primary">
      <v-tab v-for="(team, index) in teams" :key="index">
        {{ team.name }}
      </v-tab>
      <v-tab-item v-for="team in teams" :key="team.name">
        <v-row>
          <v-col cols="5">
            <team-table :team="team"></team-table>
          </v-col>
          <v-col cols="4">
            <div class="d-flex justify-center align-center calculations">
              <div>
                <p>Starting Salary Cap = ${{ team.startingSalaryCap }}</p>
                <p>Salary Cap Remaining = $</p>
                <p>Total Player Salary = $</p>
                <p>100% Tax = $</p>
                <p>200% Tax = $</p>
                <p>GRAND TOTAL = $</p>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-tab-item>
    </v-tabs>
  </v-app>
</template>

<style scoped>
.calculations {
  height: 500px;
  text-align: right;
}

p {
  font-size: 28px;
}
</style>

<script>
import TeamTable from './components/TeamTable.vue';

export default {
  components: {
    TeamTable,
  },
  data() {
    return {
      selectedTeam: '',
      teams: [
        {
          name: 'Houston Colt .45s',
          players: [],
          startingSalaryCap: 420,
        },
        {
          name: 'Brooklyn Dodgers',
          players: [],
          startingSalaryCap: 919,
        },
        {
          name: 'Detroit Stars',
          players: [],
          startingSalaryCap: 275,
        },
        {
          name: 'Zulu Cannibal Giants',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'Boston Braves',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'St. Louis Terriers',
          players: [],
          startingSalaryCap: 132,
        },
        {
          name: 'Seattle Pilots',
          players: [],
          startingSalaryCap: 777,
        },
        {
          name: 'Montreal Expos',
          players: [],
          startingSalaryCap: 730,
        },
        {
          name: 'Chicago Brownbombers',
          players: [],
          startingSalaryCap: 457,
        },
        {
          name: 'Washington Senators',
          players: [],
          startingSalaryCap: 523,
        },
        {
          name: 'California Angels',
          players: [],
          startingSalaryCap: 599,
        },
        {
          name: 'Atlanta BlackCrackers',
          players: [],
          startingSalaryCap: 168,
        },
      ],
    };
  },
  mounted() {
    this.teams = this.teams.map((team) => {
      const localStorage = JSON.parse(window.localStorage.getItem(team.name));

      if (localStorage) {
        team.players = localStorage;
      } else {
        team.players = [
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
        ];
      }
      return team;
    });
  },
  name: 'App',
};
</script>
