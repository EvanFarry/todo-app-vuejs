<template>
  <div class="modal grid">


    <!-- back button -->
    <span class="back" v-on:click="$emit('shrink-me')">
      <svg class="back-icon" width="13px" height="24px">
          <g id="backButton">
            <path d="M3.24651549,12 L12.1377551,20.8912396 C12.6441855,21.39767 12.6441855,22.218756 12.1377551,22.7251864 C11.6313247,23.2316168 10.8102387,23.2316168 10.3038083,22.7251864 L0.862244898,13.283623 C0.514748939,12.936127 0.405693318,12.4404832 0.535078036,12 C0.405693318,11.5595168 0.514748939,11.063873 0.862244898,10.716377 L10.3038083,1.27481359 C10.8102387,0.768383166 11.6313247,0.768383166 12.1377551,1.27481359 C12.6441855,1.78124401 12.6441855,2.60232996 12.1377551,3.10876039 L3.24651549,12 Z" id="Combined-Shape">
            </path>
          </g>
      </svg>
    </span>

    <!-- new title form -->
    <span class="center">
      <span v-if='showForm'>
        <input type="text"
        class="inputForm"
        autofocus
        onfocus="this.select()"
        value='title'
        v-model='newTitle'
        v-on:keyup.enter='submitNewTitle'
        >
      </span>

    <!-- list title -->
      <span v-else
        v-on:click='toggleInputForm'
        class="listTitle">{{title}}
      </span>
    </span>

    <!-- delete button -->
    <span class="delete-list" v-on:click="$emit('delete-me')">
      <svg class="delete-list-icon" width="26px" height="26px">
        <g id="delete-list-item">
          <path d="M12.2168675,12.2168675 L12.2168675,0 L14.0963855,0 L14.0963855,12.2168675 L26,12.2168675 L26,14.0963855 L14.0963855,14.0963855 L14.0963855,26 L12.2168675,26 L12.2168675,14.0963855 L0,14.0963855 L0,12.2168675 L12.2168675,12.2168675 Z" id="Combined-Shape">
          </path>
        </g>
      </svg>
    </span>


    <!-- list body -->
    <div class="listBody">
      <!-- list item -->
      <div class="item-grid" v-for='(item,index) in items' v-bind:key='items.id'>
        <span><input type="checkbox"></span>
        <span>{{item}}</span>
        <span>
          <svg class="delete-item-icon" v-on:click="deleteListItem(index)" width="19px" height="20px" viewBox="0 0 19 20" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <g id="delete-item">
              <g id="list-item" transform="translate(-236.000000, -5.000000)">
                <g id="delete-list-item" transform="translate(244.970563, 14.970563) rotate(-45.000000) translate(-244.970563, -14.970563) translate(232.970563, 2.970563)">
                  <path d="M11.2771084,11.2771084 L11.2771084,3.55271368e-15 L13.0120482,3.55271368e-15 L13.0120482,11.2771084 L24,11.2771084 L24,13.0120482 L13.0120482,13.0120482 L13.0120482,24 L11.2771084,24 L11.2771084,13.0120482 L0,13.0120482 L0,11.2771084 L11.2771084,11.2771084 Z" id="Combined-Shape"></path>
                </g>
              </g>
            </g>
          </svg>
        </span>
      </div>

      <!-- add new item textbox -->
      <div class="center">
        <input
        type="text"
        class="inputForm"
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

.center{ text-align: center; }

.modal{
  z-index: 1;
  margin: auto;
  width: 70%;
  height: 450px;
  overflow: auto;
  background-color: #73B3C2;
}

.listTitle {
  font-size: 2em;
  font-weight: 200;
  opacity: .8;
}

/* targeting Back and Delete List icons */
.back-icon, .delete-list-icon { padding-top: 8px; }

/*-- back Icon --*/
.back-icon{ fill: white; }
.back:hover{ opacity: 0.6; }

/*-- delete LIST icon --*/
.delete-list-icon{ transform: rotate(45deg); }
.delete-list-icon{ fill : red; }
.delete-list:hover{ opacity: 0.6;}

/*-- delete item icon --*/
.delete-item-icon{ fill: red; }
.delete-item-icon:hover{ opacity: 0.6;}

.inputForm{
  margin: 5px 0px 30px 0;
  width: 60%;
  padding: 5px;
  background-color: #73B3C2;
  text-align: center;
  color: white;
  font-size: 1.1em;
  outline: none;
  border: none;
  border-bottom: 2px solid white;
}
.inputForm::placeholder{
  color: white;
  opacity: 0.5;
}
.inputForm:focus::placeholder{
  color: #73B3C2;
}

/*-- top level grid --*/
.grid {
  display: grid;
  grid-template-columns: 45px 1fr 45px;
  grid-template-rows: 30px auto;
  grid-row-gap: 50px;

  padding: 10px 12px;
}

span { color: white; }
.back { text-align: left; }
.title { text-align: center; }
.delete-list {text-align: right; }

.listBody{
  grid-column: 1/4;
  grid-row: 2;
}

/*--  item-grid  --*/
.item-grid{
  display: grid;
  grid-template-columns: 20px 1fr 25px;

  margin: auto;
  width: 90%;
  padding-bottom: 25px
}

</style>
