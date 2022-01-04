<template id="task-list">
  <section class="tasks">
    <h1>
      Tasks
      <transition name="fade">
        <small v-if="incomplete">({{ incomplete }})</small>
      </transition>
    </h1>
    <div class="tasks__new input-group pull-center">
      <input
        type="text"
        class="input-group-field"
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="New task"
      />
      <span class="input-group-button">
        <button @click="addTask" class="btn btn-primary">
          <!-- <font-awesome-icon class="fas-solid fa-plus" /> -->
          Add
        </button>
      </span>
    </div>
    <div style="margin-top: 5px" class="tasks__clear btn-group pull-right">
      <button
        style="margin-right: 16px"
        class="btn btn-warning btn-sm"
        @click="$emit('clearCompleted')"
      >
        <i v-if="true" key="clearC" class="far fa-check-square"></i> Clear
        Completed
      </button>
      <div class="clearfix"></div>
      <button
        style="margin-right: 16px"
        class="btn-danger btn-sm"
        @click="$emit('clearAll')"
      >
        <font-awesome-icon icon="fa-solid fa-trash" />
        <font-awesome-icon class="fa-regular fa-trash-can-clock" />
        Clear All
      </button>
    </div>
    <div class="clear-fix"></div>
    <transition-group
      style="margin-top: 5px"
      name="fade"
      tag="ul"
      class="tasks__list no-bullet"
    >
      <task-item
        v-for="(task, index) in tasks"
        @remove="removeTask(index)"
        @complete="completeTask(task)"
        :task="task"
        :key="index"
      ></task-item>
    </transition-group>
  </section>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "TaskList",
  components: {
    TaskItem,
  },
  props: {
    tasks: { default: [] },
  },
  data() {
    return {
      newTask: "",
    };
  },
  computed: {
    incomplete() {
      return this.tasks.filter(this.inProgress).length;
    },
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false,
        });
        this.newTask = "";
      }
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    isCompleted(task) {
      return task.completed;
    },
  },
};
</script>
<style>
.tasks {
  width: 100%;
  max-width: 45rem;
  padding: 1em;
  margin: 1em auto;
  overflow: auto;
  background-color: white;
  box-shadow: 0px 0.25rem 1rem rgba(black, 0.25);
}
.tasks__list {
  clear: both;
}

body {
  background-color: #abc;
}
*,
h1,
button {
  font-family: "Nunito", sans-serif;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>