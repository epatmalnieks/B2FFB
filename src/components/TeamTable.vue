<template>
  <v-card class="mt-10" outlined>
      <v-data-table :headers="headers" hide-default-footer :items-per-page="-1"
      :items="players" fixed-header height="400px">
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
    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.players[this.editedIndex], this.editedItem);
      }
      this.close();
    },
  },
  name: 'TeamTable',
  props: {
    players: {
      required: true,
      type: Array,
    },
  },
};
</script>
