<template>
  <v-app>
    <List  :items="items" @deleteItem="deleteItem" />
  </v-app>
</template>

<script>
import List from './components/List.vue'

export default {
  name: 'App',
  components: {
   List
  },
  data () {
    return {
      items: [
          { id:1, title: 'Jason Oner', status:false},
          { id:2, title: 'Travis Howard', status:true},
          { id:3, title: 'Ali Connors', status:false },
          { id:4, title: 'Cindy Baker', status:false }
        ],
      idCount: 4
    }
  },
  methods: {
    deleteItem(id){
       const itemIndex = this.items.findIndex(el => el.id === id);
       this.items.splice(itemIndex, 1)
    }
   
  },
  computed: {
 
  }
}
</script>
