<template>
  <div>
    <form>
      <input type="text" placeholder="add New Task">
      <button value="Add">Add</button>
    </form>

    <ul class="todos">
      <li class="todo" v-for="todo in todos" :class="{ isFinished: todo.finished }">
        <label><input type="checkbox" v-model="todo.finished"> {{todo.text}}</label>
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
      ]
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
