<template>
  <div id="app">
    <task-list
      :tasks="tasks"
      @clearCompleted="clearCompletedTask()"
      @clearAll="clearAllTask()"
    ></task-list>
  </div>
</template>


<script>
import TaskList from "./components/TaskList.vue";
export default {
  name: "App",
  components: {
    TaskList,
  },
  data: function () {
    return {
      tasks: [
        {
          title: "Make todo list",
          completed: true,
        },
        {
          title: "Go skydiving",
          completed: false,
        },
      ],
    };
  },
  methods: {
    clearCompletedTask() {
      this.tasks = this.tasks.filter(this.inProgress);
      console.log(this.tasks);
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    clearAllTask() {
      this.tasks = [];
    },
    isCompleted(task) {
      return task.completed;
    },
  },
};
</script>

<style>
</style>
