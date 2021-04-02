<template>
    <div class="todoListContainer">
      <div class="heading">
        <h2 id="title">Task manager</h2>
        <add-Item-Form  v-on:reloadlist = "getList()" />
  
      </div>
          <list-View :items="items" 
                      v-on:reloadlist = "getList()"
          />
       
    </div>
</template>
<script>

import addItemForm from './addItemForm'

import listView from './listView'
export default {

components : {addItemForm ,listView } ,
data: function() {
    return {
        items : []
    }
},
methods : { 
    getList () {
    axios.get('api/items')
    .then(response => {
        this.items = response.data
    })
    .catch( error => {
        console.log(error) ;
    })

    }
},
created() {
    this.getList();
}
}
</script>

<style scoped >
.todoListContainer {
    width: 350px;
    margin: auto;
}
.heading {
 padding: 10px;
 background: #e7dfdf;

} 
#title {
    text-align: center;
     
}

</style>