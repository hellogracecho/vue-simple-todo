<template>
  <li>
    <input
      type="checkbox"
      :id="todo.id"
      :value="todo.text"
      @click="onEmitTodo"
      :class="{ checked: isChecked }"
    />
    <button @click="onRemoveTodo" class="btn--warning">Remove</button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  data() {
    return {
      isChecked: false,
    };
  },
  props: ['todo'],
  methods: {
    onEmitTodo: function(event) {
      this.$emit('clicked', {
        id: this.todo.id,
        isChecked: event.target.checked,
      });
      this.isChecked = event.target.checked;
    },
    onRemoveTodo: function() {
      this.$emit('removed', {
        id: this.todo.id,
      });
    },
  },
};
</script>

<style scoped lang="scss">
li {
  position: relative;
  button {
    position: absolute;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
  }
}
input {
  cursor: pointer;
  &[type='checkbox']:after {
    content: attr(value);
    margin: -1px 0 0 18px;
    vertical-align: top;
    white-space: nowrap;
    display: inline-block;
  }

  &.checked {
    color: #606060;
  }
}
</style>
