<template>
  <v-simple-table dense height="500px" fixed-header>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Position
            </th>
            <th class="text-left">
              Player
            </th>
            <th class="text-left">
              Salary
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in players" :key="player.player">
            <td>{{ player.position }}</td>
            <td>{{ player.name }}</td>
            <td>{{ player.salary }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
</template>

<script>
export default {
  data() {
    return {
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
    };
  },
  name: 'Home',
};
</script>
