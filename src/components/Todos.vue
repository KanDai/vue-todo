<template>
  <div>
    <div>
      <input type="text" v-model="newTask.text" placeholder="add New Task">
      <button value="Add" @click="addNewTask()">Add</button>
    </div>

    <ul class="todos">
      <li class="todo" v-for="todo in todos" :class="{ isFinished: todo.finished }">
        <label><input type="checkbox" v-model="todo.finished"> {{todo.id}} - {{todo.text}}</label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todos',
  data () {
    return {
      todos: [
        {
          id: 1,
          text: 'task1です',
          finished: false
        }, {
          id: 2,
          text: 'task2だよ',
          finished: false
        }, {
          id: 3,
          text: 'task3っすよ',
          finished: false
        }
      ],
      newTask: {
        text: ''
      }
    }
  },
  methods: {
    addNewTask () {
      if (this.newTask.text === '') return

      var newTask = {
        id: this.todos.length + 1,
        text: this.newTask.text,
        finished: false
      }

      this.todos.push(newTask)
      this.newTask.text = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style-type: none;
  padding: 0;
}


.todo.isFinished {
  text-decoration: line-through;
  color: #999;
}


</style>
