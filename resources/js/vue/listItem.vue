<template>
    <div class="item" >
        <input type="checkbox" 
        @change="updateChek()"
        v-model="item.completed"
        />

        <span :class="[item.completed ? 'completed' : '' , 'itemText']"> {{item.name}}  </span>
        <button @click="removeItem" class="trashcan"> 
          <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props : ['item'] ,
methods: {
updateChek() {
    axios.put('api/item/' + this.item.id ,{
       item : this.item
    })
    .then( response => {
        if(response.status == 200){
            this.$emit('itemchange');

        }
    })
    .catch( error => {
        console.log(error);
    })
         },
    removeItem(){
        axios.delete('api/item/' + this.item.id )
            .then( response => {
                if (response.status == 200)
                {
                   this.$emit('itemchanged'); 
                }

        })
    .catch (error => {
        console.log(error);

         })
    }
  }
}
</script>
<style  scoped>
.completed {
    text-decoration: line-through;
    color: #999999;
}
.itemText{
    width: 100%;
    margin-left: 20px;
}
.item {
    display: flex;
    justify-content: center;
    align-items: center;
}
.trashcan { 
    background: #e8b9b9e6;
    border: none;
    color: red ;
    outline: none;
    border-radius: 22px;
    padding: 6px 6px 4px 7px;
    cursor: pointer;
}
</style>