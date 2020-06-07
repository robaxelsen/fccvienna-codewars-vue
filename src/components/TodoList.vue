<template>
  <div class="todo-list">
    <h1>TODO APP</h1>
      <div>
        <input class="todo-input-add" type="text" v-model="newItemTitle">
        <button @click="addTodo">ADD</button>
      </div>
      <ul>
        <li
          v-for="(item, index) in items"
          :key="index"
        >
          <span v-if="!item.edit" @click="editTodo(index)">
            <input type="checkbox" :name="`checkbox-${index}`" :checked="item.done" @click="toggleDone(index)">
            <label :for="`checkbox-${index}`">
              {{ item.title }}
            </label>
            <button @click="removeTodo(index)">DEL</button>
          </span>
          <span v-else>WE ARE GONNA EDIT THE SHIT OUT OF THIS</span>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    msg: String
  },
  data() {
    return {
      newItemTitle: '',
      items: [
        {title: 'This is my example todo 1', done: false, edit: false},
        {title: 'This is my example todo 2', done: true, edit: false},
        {title: 'This is my example todo 3', done: false, edit: false},
        {title: 'This is my example todo 4', done: true, edit: false},
        {title: 'This is my example todo 5', done: false, edit: false},
      ]
    }
  },
  methods: {
    addTodo() {
      this.items.unshift({
        title: this.newItemTitle,
        done: false
      })
    },
    removeTodo(index) {
      this.items = this.items.filter((item, itemIndex) => {
        return itemIndex !== index
      })
    },
    toggleDone(index) {
      this.items = this.items.map((item, itemIndex) => {
        if (itemIndex === index) {
          item.done = !item.done
        }
        return item
      })
    },
    editTodo(index) {
      this.items = this.items.map((item, itemIndex) => {
        if (itemIndex === index) {
          item.edit = !item.edit
        }
        return item
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 10px;
}
a {
  color: #42b983;
}
.todo-input-add {
  margin-right: 5px;
}
</style>
