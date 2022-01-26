<template>
  <v-app>
    <v-tabs vertical dark background-color="primary">
      <v-tab v-for="(team, index) in teams" :key="index">
        {{ team.name }}
      </v-tab>
      <v-tab-item v-for="team in teams" :key="team.name">
        <v-row>
          <v-col cols="5">
            <team-table :players="team.players"></team-table>
          </v-col>
          <v-col cols="4">
            <div class="d-flex justify-center align-center calculations">
              <div>
                <p>Starting Salary Cap = $</p>
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
        },
        {
          name: 'Brooklyn Dodgers',
          players: [],
        },
        {
          name: 'Detroit Stars',
          players: [],
        },
        {
          name: 'Zulu Cannibal Giants',
          players: [],
        },
        {
          name: 'Boston Braves',
          players: [],
        },
        {
          name: 'St. Louis Terriers',
          players: [],
        },
        {
          name: 'Seattle Pilots',
          players: [],
        },
        {
          name: 'Montreal Expos',
          players: [],
        },
        {
          name: 'Chicago Brownbombers',
          players: [],
        },
        {
          name: 'Washington Senators',
          players: [],
        },
        {
          name: 'California Angels',
          players: [],
        },
        {
          name: 'Atlanta BlackCrackers',
          players: [],
        },
      ],
    };
  },
  mounted() {
    if (false) {
      console.log('erik');
    } else {
      this.teams = this.teams.map((team) => {
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
        return team;
      });
    }
  },
  name: 'App',
};
</script>
