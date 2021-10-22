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
      <button @click="addTodo(newTodo)" class="btn--primary">Add</button>
    </div>
    <ul>
      <TodoItem
        @clicked="onClickChild"
        @removed="onRemoveTodo"
        v-for="item in reversedList"
        :todo="item"
        :key="item.id"
      ></TodoItem>
    </ul>
    <pre>{{ JSON.stringify(todoList, null, ' ') }}</pre>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoItem from '@/components/TodoItem.vue';
import { todoList } from '@/data';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  props: ['checkedTodo'],
  data() {
    return {
      todoList: todoList,
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
    onRemoveTodo(selectedItem) {
      if (confirm('Are you sure you wanna delete?')) {
        this.todoList.forEach((item, index) => {
          if (item.id === selectedItem.id) {
            this.todoList.splice(index, 1);
          }
        });
      }
    },
    reOrderList: function() {
      // order by unchecked todos first followed by completed ones
      this.todoList.sort(function(x, y) {
        return x.isChecked === y.isChecked ? 0 : x.isChecked ? -1 : 1;
      });
    },
  },
  computed: {
    reversedList() {
      return [...this.todoList].reverse();
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
    margin: 16px 0;
  }

  &_add {
    display: flex;
    input {
      flex-grow: 1;
      height: 30px;
      padding: 5px 10px;
      margin-right: 10px;
      border-radius: 4px;
      border: 1px solid #00c400;
      &:focus {
        outline: none !important;
        box-shadow: 0 0 2px #00c400;
      }
    }
  }
}
pre {
  padding: 20px;
  border-radius: 4px;
  background-color: #262626;
  color: #fff;
}
</style>
