<template>
  <li>
    <input
      type="checkbox"
      :id="todo.id"
      :value="todo.text"
      @click="onEmitTodo"
    />
    <!-- <label :class="{ checked: isChecked }" for="{{ todo.id }}">{{
      todo.text
    }}</label> -->
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
  },
};
</script>

<style scoped lang="scss">
[type='checkbox']:after {
  content: attr(value);
  margin: -1px 0 0 18px;
  vertical-align: top;
  white-space: nowrap;
  display: inline-block;
}

.checked {
  text-decoration: line-through;
}
</style>
