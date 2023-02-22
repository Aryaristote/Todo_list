<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" v-model="newTask" @keyup.enter="addTask"/>
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <Task-items 
          v-for="(task, index) in tasks" 
          :key="task.id" 
          :task="task" 
          @remove="removeTask(index)" 
          @complete="completedTask(task)"
          />
          <!-- We use @name="methidName" because it's a Parent script that run in chill component  -->
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearCompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ pending }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItems from './Task-items'

export default {
  name: "Task",
  props: ['tasks'],
  components: {
    TaskItems
  },
  data() {
    return {
      newTask: "",
    }
  },
  computed: {
    pending(){
      return this.tasks.filter(this.inProgress).length;
    }
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false,
        })
      }
      this.newTask = "";
    },
    inProgress(task) {
      return !this.isCompleted(task)
    },
    isCompleted(task) {
      return task.completed;
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    removeTask(index) {
      this.tasks.splice(index, 1)
    },
    clearAll() {
      this.tasks = []
    },
    completedTask(task) {
      task.completed = !task.completed;
    }
  }
};
</script>
