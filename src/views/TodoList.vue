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
    <pre>{{ JSON.stringify(todoList, null, ' ') }}</pre>
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
        { id: 3, text: 'Eat breakfast', isChecked: false },
        { id: 4, text: 'Do laundry', isChecked: false },
        { id: 5, text: 'Vacuum', isChecked: false },
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
      this.reOrderList();
      // Clear input field
      this.newTodo = '';
    },
    onClickChild(selectedItem) {
      // update data
      this.todoList.forEach((item) => {
        if (item.id === selectedItem.id) {
          item.isChecked = selectedItem.isChecked;
        }
      });
      this.reOrderList();
    },
    reOrderList: function() {
      // order by unchecked todos first followed by completed ones
      this.todoList.sort(function(x, y) {
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
      height: 30px;
      padding: 5px 10px;
    }
    button {
      cursor: pointer;
      background-color: #00c400;
      border: transparent;
      color: #fff;
      font-weight: bold;
      border-radius: 4px;

      &:hover,
      &:focus,
      &:active {
        background-color: #0d9b0d;
      }
    }
  }
}
</style>
