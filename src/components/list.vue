<template>
  <div class="modal grid" >


    <!-- back button -->
    <span class="back" v-on:click="$emit('shrink-me')">Back</span>

    <!-- list title -->
    <span class="center">
      <span v-if='showForm'>
        <input type="text"
        autofocus
        onfocus="this.select()"
        value='title'
        v-model='newTitle'
        v-on:keyup.enter='submitNewTitle'
        >
      </span>

      <span v-else
        v-on:click='toggleInputForm'
        class="title">{{title}}
      </span>
    </span>

    <!-- delete button -->
    <span class="delete" v-on:click="$emit('delete-me')">Delete</span>


    <!-- list body -->
    <div class="listBody">

      <!-- list item -->
      <div class="item-grid" v-for='(item,index) in items' v-bind:key='items.id'>
        <span><input type="checkbox"></span>
        <span>{{item}}</span>
        <span><button type="button" v-on:click="deleteListItem(index)">delete</button> </span>
      </div>

      <!-- add new item textbox -->
      <div class="center">
        <input type="text"
        v-model='newItem'
        v-on:keyup.enter='addNewItem'
        placeholder="add new item..."
        >
      </div>

    </div>

  </div>
</template>

<script>


export default{
  name: 'List',
  data: function() {
    return{
      newItem: '',
      showForm: false,
      newTitle: this.title,
      items: this.listItems,
    }
  },
  props: [
    'title',
    'listBody',
    'listItems',
  ],

  methods: {
    toggleInputForm: function() {
      this.showForm = true;
    },
    submitNewTitle: function(){
      this.showForm = false;
      this.$emit('interface', this.newTitle)
    },
    addNewItem: function(){
      this.$emit('addNewItem', this.newItem )
      this.newItem = ''
    },
    deleteListItem: function(index){
      this.$emit('deleteListItem', this.items[index])
    },
    beforeMount: function(){
      this.newTitle = this.title
    }
  },
}
</script>


<style scoped>

.center{
  text-align: center;
}
.modal{
  z-index: 1;
  margin: auto;
  width: 70%;
  height: 450px;
  overflow: auto;
  background-color: #73B3C2;
}

/*-- top level grid --*/
.grid{
  display: grid;
  grid-template-columns: 70px 3fr 70px;
  grid-template-rows: 30px auto;
}

span { color: white; }
.back { text-align: left; }
.title { text-align: center; }
.delete {text-align: right; }

.listBody{
  grid-column: 1/4;
  grid-row: 2;
}

/*--  item-grid  --*/
.item-grid{
  display: grid;
  grid-template-columns: 20px 1fr 60px;
}

</style>
