<template>
        <div class="todo-item flex">
            <div class="a flex">
                <input type="checkbox" name="" id="" :checked="todo.completed"  @change="markItemCompleted"/>
                <div :class="['todo-name', todo.completed ? 'completed' : '']">{{todo.title}}</div>
            </div>
            <button class="delete-todo" @click="deleteItem">Delete</button>
        </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
@Component({
  components: {
  },
})
export default class TodoItem extends Vue {
    @Prop() todo!: Todo;
    @Prop() id!: number;

    markItemCompleted() {
        this.$emit('item-completed', this.$props.id);
    }
    deleteItem = () => {
      this.$emit('delete-item', this.$props.id)
    }
}
</script>
<style lang="css">
        .todo-item {
            margin: 30px 0;
            justify-content: space-between;
            font-size: 20px;
        }
        .a {
            display: flex;
            align-items: center;
        }
        .a input {
            margin-right: 10px;
        }
        .flex {
            display: flex;
        }
        .completed {
            text-decoration: line-through;
        }
</style>
