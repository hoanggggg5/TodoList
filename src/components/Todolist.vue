<template>
   <div>
       <div class="todo-list">
        <TodoItem  
            v-for="todo in todos"
            :key="todo.id"
            :id="todo.id"
            :todo="todo"
            @item-completed="markComplete"
            @delete-item="deleteTodo"
        />
        </div>
        <AddTodo @add-todo="addTodo" :idMax="todos[todos.length-1].id"/>
   </div>

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import TodoItem from './TodoItem.vue';
import AddTodo from './AddTodo.vue';
import data from './initialData';

@Component({
  components: {
    TodoItem,
    AddTodo,
  },
})
export default class Todolist extends Vue {
    todos: Array<Todo> = [
        {
            id: 1,
            title: "Learning Java",
            completed: true,
        },
        {
            id: 2,
            title: "Learning Python",
            completed: false,
        },
    ];

    markComplete(id) {
        console.log(id)
        this.todos = this.todos.map(todo => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }
    deleteTodo = id => {
        console.log(id)
        this.todos = this.todos.filter(todo => todo.id !== id)
        console.log(this.todos)
    }
    addTodo = newTodo => {
        this.todos.push(newTodo)
    }
}
</script>
<style lang="css">
    .todo-list {
        margin: 30px 0;
    }
    .flex {
        display: flex;
    }
</style>
