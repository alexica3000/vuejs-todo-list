<template>
  <div class="todo-list">
    <h2>Options</h2>
    <div class="ul-list">
      <ul class="todos">
        <li v-for="(task, index) in todos" :key="index">
          <span
              @click="toggleTaskStatus(task)"
              :class="{ completed: task.completed }"
          >{{ task.title }}</span>
          <button @click="deleteTask(task)">Delete</button>
        </li>
      </ul>
    </div>
    <input type="text" v-model="new_task" @keypress.enter="addTask"/>
    <button @click="addTask">Add</button>

    <div>
      <p><strong>Completed</strong>:{{ completedTodosCount }}</p>
      <p><strong>Pending</strong>:{{ pendingTodosCount }}</p>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        new_task: "",
        todos: [],
      };
    },
    computed: {
      completedTodosCount() {
        return this.todos.filter((task) => task.completed === true).length;
      },
      pendingTodosCount() {
        return this.todos.filter((task) => !task.completed).length;
      },
    },
    methods: {
      addTask() {
        if (this.new_task) {
          this.todos.push({title: this.new_task, completed: false});
          this.new_task = "";
        }
      },
      deleteTask(task) {
        const index = this.todos.indexOf(task);
        this.todos.splice(index, 1);
      },
      toggleTaskStatus(task) {
        task.completed = !task.completed;
      },
    },
  };
</script>

<style scoped>
  .todo-list {
    text-align: center;
    margin: 0 auto;
    width: 60%;
    border: 1px solid green;
  }

  .ul-list {
    margin: 0 auto;
    text-align: center;
  }

  .todos {
    width: 250px;
    padding: 0;
    display: inline-block;
    cursor: pointer;
  }

  .todos li {
    padding: 5px;
  }

  .todos li button {
    float: right;
  }
</style>
