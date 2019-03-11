<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="delTodo" v-on:update-todo="updtTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import Todos from '@/components/Todos.vue';
import AddTodo from '@/components/AddTodo.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  created: function() {
    this.loadData();
  },
  methods: {
    delTodo(id) {
      axios
        .delete(`http://localhost:3000/todo/${id}`)
        .then((this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      axios
        .post(`http://localhost:3000/todo`, newTodo)
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err));
    },
    updateTodo(id, updtTodo) {
      console.log(id, updtTodo);
      axios
        .patch(`http://localhost:3000/todo/${updtTodo.id}`, updtTodo)
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err));
    },
    loadData() {
      axios
        .get('http://localhost:3000/todo')
        .then(res => (this.todos = res.data))
        .catch(err => console.log(err));
    }
  },
  data() {
    return {
      todos: []
    };
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
