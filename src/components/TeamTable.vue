<template>
  <v-card class="mt-10" outlined>
      <v-data-table :headers="headers" hide-default-footer items-per-page="-1"
      :items="players" fixed-header height="350px">
        <template v-slot:item.position="{ item }">
          <span>{{item.position}}</span>
        </template>
        <template v-slot:item.name="{ item }">
          <v-text-field v-model="editedItem.name" :hide-details="true"
           dense single-line v-if="item.position === editedItem.position"></v-text-field>
          <span v-else>{{item.name}}</span>
        </template>
        <template v-slot:item.salary="{ item }">
          <v-text-field v-model="editedItem.salary" :hide-details="true"
           dense single-line v-if="item.position === editedItem.position"></v-text-field>
          <span v-else>{{item.salary}}</span>
        </template>
        <template v-slot:item.actions="{ item }">
          <div v-if="item.position === editedItem.position">
            <v-icon color="red" class="mr-3" @click="close">
              mdi-window-close
            </v-icon>
            <v-icon color="green"  @click="save">
              mdi-content-save
            </v-icon>
          </div>
          <div v-else>
            <v-icon color="green" class="mr-3" @click="editItem(item)">
              mdi-pencil
            </v-icon>
          </div>
        </template>
      </v-data-table>
    </v-card>
</template>

<script>
export default {
  created() {
    this.initialize();
  },
  data: () => ({
    defaultItem: {
      id: 0,
      name: 'New Item',
      position: 0,
      salary: 0,
    },
    editedIndex: -1,
    editedItem: {
      name: '',
      position: 0,
      salary: 0,
    },
    headers: [
      {
        text: 'Position',
        value: 'position',
      },
      {
        text: 'Name',
        value: 'name',
      },
      {
        text: 'Salary',
        value: 'salary',
      },
      {
        text: 'Actions',
        value: 'actions',
        width: '100px',
      },
    ],
    players: [],
  }),
  methods: {
    close() {
      this.editedItem = { ...this.defaultItem };
      this.editedIndex = -1;
    },
    editItem(item) {
      this.editedIndex = this.players.indexOf(item);
      this.editedItem = { ...item };
    },
    initialize() {
      this.players = [
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
      ];
    },
    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.players[this.editedIndex], this.editedItem);
      }
      this.close();
    },
  },
  name: 'TeamTable',
};
</script>
