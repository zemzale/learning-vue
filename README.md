# Learning Vue 3

## How to install vue?
 
There are 3 ways how to get vue in your project :

- Import it as CDN
- Installing it using NPM
- Use the official CLI to create scaffolding and setup the project

### How to create a new vue using the CLI?

- Install using `npm` or `yarn` 

```sh
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

- Create a new project using vue-cli

```sh
vue create <project-name>
```
- Pick configuration
- Off to working

## Basics

### Basic rendering
The basic declerative rendering example looks like : 

```html
<div id="counter">
  Counter: {{ counter }}
</div>
```
```js
const Counter = {
    data() {
        return {
            counter: 0
        }
    }
}

Vue.createApp(Counter).mount('#counter')
```

Which can be remade in the single file syntax like this
```
<template>
  <div id="counter">
    Counter : {{ counter }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
    };
  },
};
</script>
```

### Lifecycle methods
Adding lifecycle methods looks like :
```js
export default {
  data() {
    return {
      counter: 0,
    };
  },
  mounted() {
    setInterval(() => {
      this.counter += 1;
    }, 1000);
  },
};
```

### V binds
#### Attribute binding
Adding more stuff and v-binding(bind some value from vue code to an attribute) 
```html
<span v-bind:title="message"> This is an example of v-bind </span>
```
```js
  data() {
    return {
      counter: 0,
      message: `You loaded this message on ${Date().toLocaleString()}`,
    };
  },
```
#### User input handling

Adding listeners to events is easy as doing `v-on:click' 
```html
<div>
    <span v-bind:title="message"> {{ messageText }} </span>
</div>
<div>
    <button v-on:click="reverseMessage">Reverse the message above</button>
</div>
```
```js
methods: {
    reverseMessage() {
        this.messageText = this.messageText.split('').reverse().join('');
    },
},
```

Adding two-way bindings is easy too. Just gotta v-model it to input
```html
<div>
    <input v-model="messageText"/>
</div>
```


### Conditionals and loops

Conditional rendering is easily done with `v-if`.
```html
<span v-if="seen" v-bind:title="message"> {{ messageText }} </span>
```

Looping some data can be like this

```js
data() {
  return {
    todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' },
    ],
  }
}
```
```html
<ol>
    <li v-for="todo in todos" v-bind:key="todo.text">
        {{ todo.text }}
    </li>
</ol>
```


### Components

Creating a single file component works just by creating `.vue` file.
```html
<template>
    <li>{{ todo.text }}</li>
</template>
<script>
export default {
  props: [
    'todo',
  ],
};
</script>
```

Props are things that are passsed to the component using `v-bind:prop-name`. They then are available for use in the component.

To use a component in other component it needs to be imported and exposed
```js
import TodoItem from '@/components/todo-item.vue';

export default {
  components: {
    TodoItem,
  },
};
```
And then it can be used
```html
<div>
    <ol>
    <todo-item
        v-for="todo in todos"
        v-bind:todo="todo"
        v-bind:key="todo.text"
    ></todo-item>
    </ol>
</div>
```












