<template>
  <v-app>
    <v-tabs v-model="selectedTeam" background-color="primary" dark>
      <v-tab v-for="team in teams" :key="team.name">
        {{ team.name }}
      </v-tab>
    </v-tabs>
    <v-tabs-items v-model="selectedTeam">
      <v-tab-item v-for="team in teams" :key="team.name">
        <v-card flat>
          <v-card-text>{{ team.roster }}</v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      selectedTeam: '',
      tab: null,
      teams: [
        { name: 'Houston Colt .45s', roster: ' team 1 roster' },
        { name: 'Brooklyn Dodgers', roster: ' name 1 roster' },
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
};
</script>
