<template>
  <v-layout row>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-toolbar color="indigo" dark>

          <v-toolbar-title>Todo List</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon>
            <v-icon>search</v-icon>
          </v-btn>
        </v-toolbar>

        <v-list>
          <v-toolbar>
            <v-subheader flat right>
              {{ date }}
            </v-subheader>
            <v-checkbox 
            v-model="showAllItem"></v-checkbox>
          </v-toolbar>
     
          <v-list-tile
            v-for="item in shownItem"
            :key="item.title"
            avatar
          >
            <v-list-tile-action>
              <v-checkbox 
              v-model="item.status"
              ></v-checkbox>
            </v-list-tile-action>

            <v-list-tile-content>
              <v-list-tile-title v-text="item.title" :class="{checked:item.status}"></v-list-tile-title>
            </v-list-tile-content>

            <v-icon color="green" @click="dialog = true">add_circle_outline</v-icon> 
            <v-icon color="red" @click="deleteItem(item.id)">delete_outline</v-icon> 
            <v-dialog 
              v-model="dialog"
              width="500">
              <v-card>
        <v-card-title
          class="headline grey lighten-2"
          primary-title
        >
          Privacy Policy
        </v-card-title>

        <v-card-text>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            flat
            @click="dialog = false"
          >
            I accept
          </v-btn>
        </v-card-actions>
      </v-card>
            </v-dialog>
   
          </v-list-tile>
        </v-list>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import moment from 'moment'

export default {
  props:['items'],
  data() {
    return {
      showAllItem: false,
      date: moment().format("dddd, MMMM Do YYYY") ,
      dialog:false
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id)
    }
  },
  computed: {
    shownItem() {
      return this.showAllItem ? this.items.filter(el => el.status === false) : this.items
    }
  }
}
</script>

<style scoped>
  .checked {
    text-decoration: line-through;
  }
</style>
