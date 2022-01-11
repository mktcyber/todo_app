<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
             <add-item
                v-on:reloadlist="getList()"/>
        </div>
        <list-view 
        :todo_items='todo_items'
        v-on:reloadlist="getList()"/>
    </div> 
</template>
<script>
import addItem from "./addItem"
import listView from './listView' 
export default {
    components:{
        addItem,
        listView 
    },
    data: function(){
        return {
            todo_items:[]
        }
    },
    methods: {
        getList(){
            axios.get('api/todo_items')
            .then( response =>{
                this.todo_items = response.data
            })
            .catch( error =>{
                console.log( error  )
            })
        }
    }, 
    created(){
        this.getList(); 
    }
}
</script>

<style scoped>
.todoListcontainer{
    width: 350;
    margin: auto;
}
.heading{
    background: #e6e6e6;
    padding: 10px;
}
#title{
    text-align: center;
}
</style>