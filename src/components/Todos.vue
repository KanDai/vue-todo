<template>
  <div>
    <div class="form">
      <input type="text" v-model="newTask.text" placeholder="Add New Task">
      <button value="Add" @click="addNewTask()">Add</button>
    </div>

    <ul class="todos">
      <li class="todo" v-for="todo in filteredTodos" :class="{ isFinished: todo.finished }">
        <label><input type="checkbox" v-model="todo.finished">{{todo.text}}</label>
        <button value="delete" @click="removeTask(todo)">× 削除</button>
      </li>
    </ul>

    <div>
      <h3>設定</h3>
      <label><input type="checkbox" @change="saveSetting" v-model="setting.showFinishedItem">終了したタスクを表示</label>
    </div>
  </div>
</template>

<script>

var STORAGE_KEY = 'vue-todo'
var STORAGE_KEY_SETTING = 'vue-todo-setting'
var DEFAULT_SETTING = {
  showFinishedItem: true
}

export default {
  name: 'todos',
  data () {
    return {
      todos: JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'),
      setting: JSON.parse(localStorage.getItem(STORAGE_KEY_SETTING)) || DEFAULT_SETTING,
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
    },
    removeTask (todo) {
      this.todos.splice(this.todos.indexOf(todo), 1)
    },
    saveSetting () {
      localStorage.setItem(STORAGE_KEY_SETTING, JSON.stringify(this.setting))
    }
  },
  computed: {
    filteredTodos: function () {
      var setting = this.setting
      return this.todos.filter(function (todo) {
        if (setting.showFinishedItem) {
          return todo
        } else if (todo.finished === false) {
          return todo
        }
      })
    }
  },
  watch: {
    todos: {
      handler: function (todos) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(todos))
      },
      deep: true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3 {
  margin: 0 0 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

.form {
  display: flex;  
}
.form input {
  width: 100%;
  margin-right: 10px;
  padding: 10px;
  appearance: none;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 6px;
}
.form button {
  padding: 10px 30px;
  appearance: none;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 6px;
}

.todos {
  border: 1px solid #ddd;
  border-radius: 6px;
  width: 100%;
}

.todo {
  padding: 12px;
  display: flex;
}
.todo:not(:last-child) {
  border-bottom: 1px solid #ddd;
}

.todo input {
  margin-right: 10px;
}
.todo label {
  display: block;
  width: 100%;
}
.todo.isFinished {
  background: #eee;
}
.todo.isFinished label {
  text-decoration: line-through;
  color: #999;
}

.todo button {
  display: block;
  margin-left: auto;
  white-space: nowrap;
  appearance: none;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 4px;
}

</style>
