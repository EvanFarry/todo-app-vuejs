<template>
  <div id="app">

    <!-- Headers -->
    <h1 v-if='lists.length>0'>Your Check Lists</h1>
    <h1 v-else>Add New Check List</h1>

    <!-- List of Lists -->
    <div v-for="(list, index) in lists" v-bind:key='list.id'>

      <div>

        <!-- expanded model-->
        <div v-if='list.expand' >
          <List
            v-on:delete-me='deleteList(index)'
            v-on:shrink-me='shrink(index)'
            v-bind:title='list.title'
            v-bind:listBody='list.body'
            @interface='list.title = $event'
            >
          </List>
        </div>

        <!-- minimized list item -->
        <div
          v-else
          class="mini"
          v-on:click="expand(index)">
          {{list.title}}
        </div>

      </div>

    </div>


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
      this.lists.push(
        {
          expand: false,
          title: 'New List',
          body: 'This is a List body',
          toDoItems: []
        }
      );
    },
    deleteList: function(index){
      this.lists.splice(index,1);
    },
    expand: function(index){
      this.lists[index].expand = true;
    },
    shrink: function(index){
      this.lists[index].expand = false;
    },
    childDataHandler: function(event){
      console.log('child data handler? idk', event);
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

@media only screen and (min-width: 800px){ #app { width: 80%; }}

@media only screen and (min-width: 900px){ #app { width: 70%; }}

@media only screen and (min-width: 1200px){ #app { width: 50%; }}


h1{
  font-family: 'Avenir';
  font-weight: 200;
  text-align: center;
  color: #73B3C2;
  margin-bottom: 45px;
}

.mini {
  width: 80%;
  margin: auto;
  text-align: center;
  background-color: #5FA6B7;
  color: white;
  padding: 8px 0px;
  margin-bottom: 20px;
}

.addListButton{
  text-align: center;
  margin-top: 30px;
}

</style>
