<template>
  <div class="list">

    <div v-if='expanded'>
      <div class="modal">
        <div class="grid">
          <span class="back" v-on:click='toggleExpand'>Back</span>
          <span class="title">{{title}}</span>
          <span class="delete">Delete</span>
          <ListBody class="listBody"></ListBody>
        </div>
      </div>
    </div>

    <div class="mini" v-else v-on:click='toggleExpand'>
      <h2>{{title}}</h2>
    </div>

  </div>
</template>

<script>

import ListBody from './list-body.vue'

export default{
  name: 'List',
  components: {
    ListBody,
  },
  data : () => {
    return{
      title: 'New List',
      expanded: false,
      newItem: '',
      items: [
        {
          checkBoxValue: false,
          itemBody: 'make a to do app',
        }
      ],
    }
  },
  props: {
    inputData: '',
  },
  methods: {
    addItem: function(){
      this.items.push({
        checkBoxValue: false,
        itemBody: this.newItem
      }
      )
      this.newItem = ''
    },
    removeItem: function(index){
      //console.log('Remove index : ' + index);
      this.items.splice(index, 1)
    },
    toggleExpand: function(){
      this.expanded = !this.expanded
    }
  },
}
</script>


<style scoped>

.mini {
  width: 80%;
  margin: auto;
  text-align: center;
  background-color: #5FA6B7;
  color: white;
  padding: 8px 0px;
  margin-bottom: 20px;
}

.modal{
  z-index: 1;
  margin: auto;
  width: 70%;
  height: 450px;
  overflow: auto;
  background-color: #73B3C2;
}

.grid{
  display: grid;
  grid-template-columns: 70px 3fr 70px;
}

span{ color: white; }
.back { text-align: left; }
.title { text-align: center; }
.delete {text-align: right; }

.listBody{
  padding-top: 50px;
  grid-column: 1/4;
  grid-row: 2;
}

</style>
