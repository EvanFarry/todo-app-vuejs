<template>
  <div class="modal grid" >

    <!-- back button -->
    <span class="back" v-on:click="$emit('shrink-me')">Back</span>


    <!-- list title -->
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
      class="title"
      >{{title}}
    </span>

    <!-- delete button -->
    <span class="delete" v-on:click="$emit('delete-me')">Delete</span>

    <!-- list body -->
    <div class="listBody">{{listBody}}</div>

  </div>
</template>

<script>


export default{
  name: 'List',
  data: function() {
    return{
      showForm: false,
      newTitle: this.title,
    }
  },
  props: [
    'title',
    'listBody'
  ],

  methods: {
    toggleInputForm: function() {
      this.showForm = true;
    },
    submitNewTitle: function(){
      this.showForm = false;
      this.$emit('interface', this.newTitle)
    },
    beforeMount: function(){
      this.newTitle = this.title
      console.log('premont');
    }
  },
}
</script>


<style scoped>


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
  grid-template-rows: 30px auto;
}

span{ color: white; }
.back { text-align: left; }
.title { text-align: center; }
.delete {text-align: right; }

.listBody{
  grid-column: 1/4;
  grid-row: 2;
}

</style>
