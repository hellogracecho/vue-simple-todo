<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/todo-list">TodoList</router-link>
  </div>
  <router-view />
</template>

<style lang="scss">
#app {
  font-family: Courier New, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #1a1a1a;
  padding: 0 30px;
}

#nav {
  text-align: center;
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
}

#nav a.router-link-exact-active {
  color: #3cac3c;
}

pre {
  white-space: pre-wrap; /* css-3 */
  white-space: -moz-pre-wrap; /* Mozilla, since 1999 */
  white-space: -pre-wrap; /* Opera 4-6 */
  white-space: -o-pre-wrap; /* Opera 7 */
  word-wrap: break-word; /* Internet Explorer 5.5+ */
}

button {
  cursor: pointer;
  padding: 10px 20px;
  width: 100px;
  border: transparent;
  color: #fff;
  font-weight: bold;
  border-radius: 4px;
  &.btn--primary {
    background-color: #00c400;

    &:hover,
    &:focus,
    &:active {
      background-color: #0fa90f;
    }
  }
  &.btn--warning {
    padding: 6px 20px;
    color: #c4280d;
    background: #fff;
    border: 1px solid #c4280d;

    &:hover,
    &:focus,
    &:active {
      color: #fff;
      background-color: #c4280d;
    }
  }
}
</style>
