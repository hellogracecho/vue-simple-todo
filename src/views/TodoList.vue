<template>
  <div class="todo-list">
    <h1>✅ TODO List</h1>
    <div class="todo-list_add">
      <input v-model.trim="newTodo" type="text" placeholder="Add new todo" />
      <button @click="addTodo(newTodo)">Add</button>
    </div>
    <ul>
      <TodoItem
        @clicked="onClickChild"
        v-for="item in groceryList"
        :todo="item"
        :key="item.id"
      ></TodoItem>
    </ul>
    <p>Raw Data:</p>
    <pre>{{ JSON.stringify(groceryList) }}</pre>
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
      groceryList: [
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

      this.groceryList.push({ id: uid, text: newTodo, isChecked: false });
      this.newTodo = '';
    },
    onClickChild(selectedItem) {
      // console.log(selectedItem.id);
      this.groceryList.forEach((item) => {
        if (item.id === selectedItem.id) {
          item.isChecked = selectedItem.isChecked;
        }
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
