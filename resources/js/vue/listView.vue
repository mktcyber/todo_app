<template>
    <div>
        <div v-for="(todo_item, index) in todo_items" :key="index">
            <list-item
                :todo_item="todo_item"
                class="todo"
                v-on:itemchanged= "$emit('reloadlist')"
                />
        </div>
    </div>
</template>

<script>
import listItem from './listItem' 
import ListItem from './listItem.vue' 
export default { 
    props:['todo_items'],
    components: {
        listItem
    }
}
</script>
<style scoped>
.todo{
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}
</style>