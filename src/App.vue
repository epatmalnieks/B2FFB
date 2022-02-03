<template>
  <v-app>
    <v-tabs vertical dark background-color="primary">
      <v-tab v-for="(team, index) in teams" :key="index" :class="{'division-divider': index === 3 || index === 7}">
        <v-img contain height="30" width="30" :src="getLogo(team.logo)"></v-img>
        <span class="team-name">{{ team.name }}</span>
      </v-tab>
      <v-tab-item v-for="team in teams" :key="team.name">
        <v-row>
          <v-col cols="5">
            <team-table :team="team"></team-table>
          </v-col>
          <v-col cols="6">
            <v-img contain height="200" class="mt-4" :src="getLogo(team.logo)"></v-img>
            <p class="d-flex justify-center">{{ team.owner }}</p>
            <div class="d-flex justify-center mt-6 calculations">
              <v-card elevation="15" outlined class="pa-4">
                <p class="mb-2">Starting Salary Cap = {{ formatPrice(team.startingSalaryCap) }}</p>
                <p class="mb-2">Total Player Salary = {{ formatPrice(getTotalPlayerSalary(team.players)) }}</p>
                <p class="mb-2">Salary Cap Remaining = <span :class="{'red--text': getSalaryCapRemaining(team) < 0}">{{ formatPrice(getSalaryCapRemaining(team)) }}</span></p>
                <p class="mb-2">100% Tax = {{ formatPrice(get100Tax(team)) }}</p>
                <p class="mb-1">200% Tax = {{ formatPrice(get200Tax(team)) }}</p>
                <p class="grand-total pt-1">GRAND TOTAL = {{ formatPrice(getGrandTotal(team)) }}</p>
              </v-card>
            </div>
          </v-col>
        </v-row>
      </v-tab-item>
      <div class="d-flex justify-center mt-16">
        <v-btn width="100px" color="error" @click="clearClicked">Clear</v-btn>
      </div>
    </v-tabs>
  </v-app>
</template>

<style scoped>
p {
  font-size: 28px;
}

.calculations {
  text-align: right;
}

.division-divider {
  border-bottom: 1px solid white;
}

.grand-total {
  border-top: 3px solid black;
}

.team-name {
  margin-left: 8px;
  min-width: 205px;
  text-align: left;
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
          logo: 'dodgers',
          name: 'Brooklyn Dodgers',
          owner: 'Erik',
          players: [],
          startingSalaryCap: 127,
        },
        {
          logo: 'colt45s',
          name: 'Houston Colt .45s',
          owner: 'Adam',
          players: [],
          startingSalaryCap: 425,
        },
        {
          logo: 'stars',
          name: 'Detroit Stars',
          owner: 'Chris',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'giants',
          name: 'Zulu Cannibal Giants',
          owner: 'Bob',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'braves',
          name: 'Boston Braves',
          owner: 'Dave/Tyler',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'terriers',
          name: 'St. Louis Terriers',
          owner: 'Chet',
          players: [],
          startingSalaryCap: 371,
        },
        {
          logo: 'pilots',
          name: 'Seattle Pilots',
          owner: 'Jay',
          players: [],
          startingSalaryCap: 430,
        },
        {
          logo: 'expos',
          name: 'Montreal Expos',
          owner: 'Tom',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'brownbombers',
          name: 'Chicago Brownbombers',
          owner: 'Gabe',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'senators',
          name: 'Washington Senators',
          owner: 'Justin',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'angels',
          name: 'California Angels',
          owner: 'Victor',
          players: [],
          startingSalaryCap: 500,
        },
        {
          logo: 'blackcrackers',
          name: 'Atlanta BlackCrackers',
          owner: 'Bill',
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
    getLogo(name) {
      return require(`./assets/${name}.jpg`);
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
