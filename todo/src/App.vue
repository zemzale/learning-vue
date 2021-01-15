<template>
  <div id="counter">
    <div>
      Counter : {{ counter }}
    </div>
    <div>
      <span v-if="seen" v-bind:title="message"> {{ messageText }} </span>
    </div>
    <div>
      <button v-on:click="reverseMessage">Reverse the message above</button>
    </div>
    <div>
      <input v-model="messageText"/>
    </div>
    <div>
      <ol>
        <li v-for="todo in todos" v-bind:key="todo.text">
          {{ todo.text }}
        </li>
      </ol>
    </div>
    <div>
      <ol>
        <todo-item
          v-for="todo in todos"
          v-bind:todo="todo"
          v-bind:key="todo.text"
        ></todo-item>
      </ol>
    </div>
  </div>
</template>

<script>
import TodoItem from '@/components/todo-item.vue';

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      counter: 0,
      message: `You loaded this message on ${Date().toLocaleString()}`,
      messageText: 'This is an example of v-bind',
      seen: true,
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' },
      ],
    };
  },
  mounted() {
    setInterval(() => {
      this.counter += 1;
    }, 1000);
  },
  methods: {
    reverseMessage() {
      this.messageText = this.messageText.split('').reverse().join('');
    },
  },
};
</script>

<style>
</style>
