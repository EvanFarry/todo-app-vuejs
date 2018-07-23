<template>
  <div class="list-body">

    <div v-for="(item, index) in items" :key='item.id'>
      <span> <input type="checkbox"> </span>
      <span>{{item.itemBody}}</span>
      <button type="button" v-on:click="removeItem(index)">Remove</button>
    </div>

    <input type="text"
    v-model='newItem'
    v-on:submit="addItem"
    v-on:keyup.enter='addItem'
    >
    <button type="button" v-on:click='addItem'>Add item</button>

  </div>
</template>

<script>

export default{
  name: 'ListBody',
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
      })
      this.newItem = ''
    },
    removeItem: function(index){
      //console.log('Remove index : ' + index);
      this.items.splice(index, 1)
    },
  },
}
</script>


<style scoped>

.list-body{
  margin: auto;
  width: 90%;
}

</style>
