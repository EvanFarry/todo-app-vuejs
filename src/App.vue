<template>
  <div id="app">

    <!-- Headers -->
    <h1 v-if='lists.length>0'>Your Check Lists</h1>
    <h1 v-else>Add New Check List</h1>

    <!-- List of Lists -->
    <div v-for="(list, index) in lists" v-bind:key='list.id'>
      <div>
        <!-- expanded modal -->
        <div v-if='list.expand' >
          <List
            v-on:delete-me='deleteList(index)'
            v-on:shrink-me='shrink(index)'
            v-bind:title='list.title'
            v-bind:listBody='list.body'
            v-bind:listItems='list.toDoItems'
            v-on:interface='list.title = $event'
            v-on:addNewItem='addListItem($event, index)'
            v-on:deleteListItem='deleteListItem($event, index)'
            >
          </List>
        </div>

        <!-- minimized list item -->
        <div
          v-bind:class="{ 'hide' : isModal }"
          v-else
          class="mini"
          v-on:click="expand(index)">
          <span>{{list.title}}</span>
        </div>

      </div>
    </div><!-- end v-for -->


    <!-- add new list button -->
    <div class="addListButton" v-bind:class="{ 'hide' : isModal }">
      <svg width="50px"
           height="50px"
           v-on:click='addNewList'
           >
        <g id="newListSvg">
          <g>
            <circle id="Oval" fill="#8ED9E0" cx="25" cy="25" r="25"></circle>
            <path d="M28.212766,22.287234 L38.5,22.287234 L38.5,27.712766 L28.212766,27.712766 L28.212766,38 L22.787234,38 L22.787234,27.712766 L12.5,27.712766 L12.5,22.287234 L22.787234,22.287234 L22.787234,12 L28.212766,12 L28.212766,22.287234 Z" id="Combined-Shape" fill="#FFFFFF"></path>
          </g>
        </g>
      </svg>
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
      lists: [],
      isModal: false,
    }
  },
  computed: {

  },
  methods: {
    addNewList: function(){
      this.lists.push(
        {
          expand: false,
          title: 'New List',
          toDoItems: []
        }
      );
    },
    deleteList: function(index){
      this.lists.splice(index,1);
      this.isModal = !this.isModal;
    },
    addListItem: function(e, index){
      this.lists[index].toDoItems.push(
        {
          "checked":false,
          "body":e,
        }
      );
    },
    deleteListItem: function(e, index){
      let i = this.lists[index].toDoItems.indexOf(e);
      this.lists[index].toDoItems.splice(i,1);
    },
    expand: function(index){
      this.lists[index].expand = true;
      this.isModal = !this.isModal;
    },
    shrink: function(index){
      this.lists[index].expand = false;
      if (this.isModal == true) {
        this.isModal = !this.isModal;
      }
    },
    shrinkAll: function(){
      for (var i = 0; i < this.lists.length; i++) {
        this.shrink(i);
      }
    },
  },
  mounted() {
    if (localStorage.getItem('lists')) {
      this.lists = (JSON.parse(localStorage.getItem('lists')));
    }
    /* shrink all modals on refresh  */
    this.shrinkAll();
  },
  watch: {
    lists: {
      handler(){
        localStorage.setItem('lists', JSON.stringify(this.lists));
      },
      deep: true
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', 'Helvetica', 'Arial', 'sans-serif';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px auto;
}

@media only screen and (min-width: 800px){ #app { width: 80%; }}

@media only screen and (min-width: 900px){ #app { width: 70%; }}

@media only screen and (min-width: 1200px){ #app { width: 50%; }}


h1{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-weight: 200;
  text-align: center;
  color: #73B3C2;
  margin-bottom: 45px;
}

.mini {
  width: 70%;
  margin: auto;
  text-align: center;
  background-color: #5FA6B7;
  border-radius: 3px;
  color: white;
  padding: 8px 0px;
  margin-bottom: 20px;
  transition: width .1s;
}

.mini > span {
  font-size: 1.3rem;
  letter-spacing: 1px;
  opacity: .8;
}

.mini:hover{
  width: 75%;
  cursor: pointer;
}

.addListButton{
  text-align: center;
  margin-top: 30px;
}





.hide{ display: none; }

</style>
