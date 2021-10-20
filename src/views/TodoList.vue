<template>
  <div class="todo-list">
    <h1>✅ TODO List</h1>
    <div class="todo-list_add">
      <input
        @keyup.enter="addTodo(newTodo)"
        v-model.trim="newTodo"
        type="text"
        placeholder="Add new todo"
      />
      <button @click="addTodo(newTodo)">Add</button>
    </div>
    <ul>
      <TodoItem
        @clicked="onClickChild"
        v-for="item in todoList"
        :todo="item"
        :key="item.id"
      ></TodoItem>
    </ul>
    <p>Raw Data:</p>
    <pre>{{ JSON.stringify(todoList) }}</pre>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoItem from '@/components/TodoItem.vue';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  props: ['checkedTodo'],
  data() {
    return {
      todoList: [
        { id: 0, text: 'Wake up in the morning', isChecked: false },
        { id: 1, text: 'Brush my teeth', isChecked: false },
        { id: 2, text: 'Wash your face', isChecked: false },
      ],
      newTodo: '',
      checkedTodos: [],
    };
  },
  methods: {
    addTodo: function(newTodo) {
      if (!newTodo) {
        return;
      }
      let uid = Date.now();

      this.todoList.push({ id: uid, text: newTodo, isChecked: false });
      // re-order list by Unchecked to Checked
      this.reOrderList();
      this.newTodo = '';
    },
    onClickChild(selectedItem) {
      // update data
      this.todoList.forEach((item) => {
        if (item.id === selectedItem.id) {
          item.isChecked = selectedItem.isChecked;
        }
      });
      // re-order list by Unchecked to Checked
      this.reOrderList();
    },
    reOrderList: function() {
      this.todoList.sort(function(x, y) {
        // false values first
        return x.isChecked === y.isChecked ? 0 : x.isChecked ? 1 : -1;
      });
    },
  },
};
</script>

<style scope lang="scss">
.todo-list {
  ul {
    text-align: left;
    list-style: none;
    padding: 0;
  }
  li {
    margin: 10px 0;
  }

  &_add {
    display: flex;
    input {
      flex-grow: 1;
    }
  }
}
</style>
