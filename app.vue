<template>
  <div class="container">
  <div>
    <h1>Todo List</h1>
    <div v-if="tasks.length === 0" class="empty-task">Belum ada Task</div>
    <div v-else>
    <div class="list-task">
      <div class="item-task d-flex align-items-start border-bottom pt-3 pb-4" v-for="task in tasks" :key="task.id">
        <input type="checkbox" name="status" class="me-2 mt-2" v-model="task.isDone">
        <div class="d-flex flex-column">
          <div class="title-task mb-1" :class="{'task-done': task.isDone}">{{ task.title }}</div>
          <div class="description-task small text-muted">{{ task.description }}</div>
          <div>
            <a href="#" class="delete-button" @click="deleteTask(task.id)">Delete</a>
          </div>
        </div>
      </div>
    </div>
  </div>
    <div class="action py-2">
      <a href="#" class="add-button" v-if="!isCreating" @click="isCreating = !isCreating">Add Task</a>
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input v-model="titleValue" class="form-control border-0 mb-2" placeholder="Title" type="text">
            <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="addTask">Save</button>
          <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      isCreating: false,
      isDelete: false,
      titleValue: '',
      descriptionValue: '',
      tasks: [],
    }
  },
  methods: {
    addTask() {
      console.log('title: ', this.titleValue);
      console.log('description: ', this.descriptionValue);
      this.tasks.unshift({
        id: this.tasks.length + 1,
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
     
      this.isCreating = false;
      this.titleValue = '';
      this.descriptionValue = '';
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    toggleTaskStatus(task){
      task.isDone = !task.isDone;
    }
  }
};
</script>
<style>
  .task-done{
    text-decoration: line-through;
  }
</style>