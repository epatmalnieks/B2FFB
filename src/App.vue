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
                <p>Starting Salary Cap = {{ formatPrice(team.startingSalaryCap) }}</p>
                <p>Total Player Salary = {{ formatPrice(getTotalPlayerSalary(team.players)) }}</p>
                <p>Salary Cap Remaining = <span :class="{'red-text': getSalaryCapRemaining(team) < 0}">{{ formatPrice(getSalaryCapRemaining(team)) }}</span></p>
                <p>100% Tax = {{ formatPrice(get100Tax(team)) }}</p>
                <p>200% Tax = {{ formatPrice(get200Tax(team)) }}</p>
                <p>GRAND TOTAL = {{ formatPrice(getGrandTotal(team)) }}</p>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-tab-item>
      <v-spacer></v-spacer>
      <div class="d-flex justify-center mb-6">
        <v-btn width="100px" color="error" @click="clearClicked">Clear</v-btn>
      </div>
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

.red-text {
  color: red;
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
          startingSalaryCap: 425,
        },
        {
          name: 'Brooklyn Dodgers',
          players: [],
          startingSalaryCap: 127,
        },
        {
          name: 'Detroit Stars',
          players: [],
          startingSalaryCap: 500,
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
          startingSalaryCap: 371,
        },
        {
          name: 'Seattle Pilots',
          players: [],
          startingSalaryCap: 430,
        },
        {
          name: 'Montreal Expos',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'Chicago Brownbombers',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'Washington Senators',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'California Angels',
          players: [],
          startingSalaryCap: 500,
        },
        {
          name: 'Atlanta BlackCrackers',
          players: [],
          startingSalaryCap: 500,
        },
      ],
    };
  },
  methods: {
    clearClicked() {
      if (window.confirm('Are you sure you want to clear everything?')) {
        window.localStorage.clear();
        this.init();
      }
    },
    formatPrice(value) {
      const formatter = new Intl.NumberFormat('en-US', {
        currency: 'USD',
        minimumFractionDigits: 0,
        style: 'currency',
      });
      return formatter.format(value);
    },
    get100Tax(team) {
      if (this.getSalaryCapRemaining(team) < 0) {
        const taxableAmount = this.getTotalPlayerSalary(team.players) - team.startingSalaryCap;
        return taxableAmount > 100 ? 100 : taxableAmount;
      }
      return 0;
    },
    get200Tax(team) {
      if (this.getSalaryCapRemaining(team) < -100) {
        let taxableAmount = this.getTotalPlayerSalary(team.players) - team.startingSalaryCap;
        taxableAmount -= 100;
        return taxableAmount * 2;
      }
      return 0;
    },
    getGrandTotal(team) {
      return this.getTotalPlayerSalary(team.players) + this.get100Tax(team) + this.get200Tax(team);
    },
    getSalaryCapRemaining(team) {
      return team.startingSalaryCap - this.getTotalPlayerSalary(team.players);
    },
    getTotalPlayerSalary(players) {
      return players.map((player) => parseInt(player.salary, 10)).reduce((prev, curr) => prev + curr, 0);
    },
    init() {
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
  },
  mounted() {
    this.init();
  },
  name: 'App',
};
</script>
