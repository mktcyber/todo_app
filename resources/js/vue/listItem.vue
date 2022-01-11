<template>
    <div class="todo">
        <input type="checkbox"
        @change="updateCheck()"
        v-model="todo_item.completed"/>
        <span :class="[todo_item.completed ? 'completed': '', 'todotext']">{{todo_item.todo_item}}</span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon='trash'/>
        </button>
    </div>
</template>
<script>
export default {
    props:["todo_item"],
    methods: {
        updateCheck(){
            axios.put('api/todo_item/' + this.todo_item.id, {
                todo_item: this.todo_item
            })
            .then( response =>{
                if( response.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch( error =>{
                console.log( error );
            })
        },
        removeItem(){
            axios.delete('api/todo_item/' + this.todo_item.id )
            .then( response =>{
                if( response.status==200){
                    this.$emit('itemchanged');
                }
            })
            .catch( error =>{
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color: #9999;
}
.todoText{
    width: 100%;
    margin-left: 20px;
}
.todo {
    display: flex;
    justify-content: center;
    align-items: center;
}
.trashcan{
    background: #e6e6e6;
    border: none;
    color: #FF0000;
    outline: none;
}
</style>