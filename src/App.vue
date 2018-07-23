<template>
  <div id="app">

    <!-- Headers -->
    <h1 v-if='lists.length>0'>Your Check Lists</h1>
    <h1 v-else>Add New Check List</h1>

    <!-- List of Lists -->
    <div ref='target'></div>

    <!-- add new list button -->
    <div class="addListButton">
      <img src="./assets/newListButton@3x.png"
       v-on:click='addNewList'
       height="50px"
       width="50px">
     </div>

  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Vue from 'vue'
import List from './components/list.vue'

export default {
  name: 'app',
  components: {
    List,
  },
  data: function(){
    return{
      lists: []
    }
  },
  methods: {
    // reference : https://codesandbox.io/embed/4l3w20zomw
    addNewList: function(){
      let ComponentClass = Vue.extend(List);
      let instance = new ComponentClass({});
      this.lists.push(instance);
      instance.$mount();
      this.$refs.target.appendChild(instance.$el);
    },
    deleteList: function(){
      //
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px auto;
}

@media only screen and (min-width: 800px){
  #app { width: 80%; }
}

@media only screen and (min-width: 900px){
  #app { width: 70%; }
}

@media only screen and (min-width: 1200px){
  #app { width: 50%; }
}


h1{
  font-family: 'Avenir';
  font-weight: 200;
  text-align: center;
  color: #73B3C2;
  margin-bottom: 45px;
}

.addListButton{
  text-align: center;
  margin-top: 30px;
}

</style>
