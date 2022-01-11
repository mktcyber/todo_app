<template>
     <div class="addItem">
          <input type="text" v-on:keyup.13="addItem" v-model="item.todo_name"/> 
          <font-awesome-icon
          icon='plus-square'
          @click="addItem()"
          :class="[ item.todo_name ? 'active': 'inactive', 'plus']"/>
     </div>
</template>

 <script>
 export default {
     data: function(){
         return {
             item:{
                 todo_name:''
             }
         }
     },
     methods:{
         addItem(){
             if(this.item.todo_name == ''){
                 return;
             }

             axios.post('api/todo_item/store',{
                 item: this.item
             })
             .then( response => {
                 if( response.status == 201){
                     this.item.todo_name="";
                     this.$emit('reloadlist')
                 }
             })
             .catch( error => {
                 console.log( error );
             })
         }
     }
 }
 </script>
 
<style scoped>
    .addItem{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input{
        background: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin-right: 10px;
        width: 100%;

    }
    .plus{
        font-size: 20px;
    }
    .active{
        color:#00CE25;
    }
    .inactive{
        color: #9999;
    }
</style>