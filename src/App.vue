<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <!-- List Of Cards (all cards is here) -->
        <Card 
          title="To Do" 
          :list="list1" 
          @onRemoveCard="removeCardFromList"/>
        <Card 
          title="In Progress" 
          :list="list2" 
          @onRemoveCard="removeCardFromList"/>
        <Card 
          title="Done" 
          :list="list3" 
          @onRemoveCard="removeCardFromList"/>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  name: 'app',
  components: {
    Card
  },
  data () {
    return {
      list1: [
        { text: "Do this" },
        { text: "Do something else" }
      ],
      list2: [
        { text: "Do that" },
        { text: "Do something else again" }
      ],
      list3: []
    }
  },
  methods: {
    removeCardFromList (data) {
      if (data.title === "To Do") this.list1 = this.listFilter(this.list1, data.index);
      if (data.title === "In Progress") this.list2 = this.listFilter(this.list2, data.index);
      else this.list3 = this.listFilter(this.list3, data.index);
    },
    listFilter (list, index) {
      return list.filter((item, i) => {
          if (i != index) return item;
      })
    }
  }
}
</script>

<style>
  html, body, #app, .container {
    background-color: #0A74A2;
  }
  #app {
    margin-top: 5%;
  }
</style>
