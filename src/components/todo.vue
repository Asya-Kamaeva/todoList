<template lang="pug">
    div
        .todo__title Чем займемся сегодня? 
        .todo__content
            
            todoInput(
                @addTodo="addTodo"
            )
            todoList(
                v-if="todos.length > 0"
                :todos="filteredTodos"
                @removeTodo="removeTodo"
                @checkTodo="checkTodo"
                @filterTodos="filterTodos"
            )
        //- pre {{filter}}
        //- pre {{todos}}  

</template>

<script>
import todoInput from './todoInput';
import todoList from './todoList';

export default {
    data(){
        return{
            todos: [],
            filter: 'all'
        }
    },
    components: {
        todoInput, todoList
    },
    computed:{
        filteredTodos(){
            switch(this.filter){
                case 'all':
                    return this.todos;
                case 'active':
                    return this.todos.filter(item => item.checked === false);
                case 'completed':
                    return this.todos.filter(item => item.checked);
            }
        }
    },
    methods: {
        addTodo(todo){
            this.todos.push(todo);
        },
        removeTodo(todoId){
            this.todos=this.todos.filter(item => item.id !== todoId);
        },
        checkTodo(todo){
            this.todos = this.todos.map(item => (item.id === todo.id ? todo : item))
        },
        filterTodos(filter){
            this.filter = filter;
        }
    }
}
</script>

<style lang="scss" scoped>

.todo{

    &__title{
        font-size: 24px;
        margin-top: 100px;
        color: #305985;
        font-weight: normal;

    }

    &__content{
    margin-top: 15px;
    background: #fff;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
    }
    
}

</style>
