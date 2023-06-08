<template>
  <div class="list-task" style="margin-top: 10px; margin-left: 10px;">
    <h3>Todo List</h3>
    <div v-if="tasks.length > 0">
      <div v-for="item of tasks" :key="item.id" :class="['item-task d-flex align-items-start border-bottom pt-3 pb-4',
        isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12']">
        <input type="checkbox" name="status" id="task" class="me-2 mt-2" :checked="item.isDone" v-model="item.isDone">
        <div class="d-flex flex-column">
          <div :class="['title-task mb-1', item.isDone ? 'text-decoration-line-through fst-italic' : '']">
            {{ item.title }}
          </div>
          <div class="description-task small text-muted">
            {{ item.description }}
          </div>
          <a href="#" class="delete-button text-danger mt-3" @click="deleteTask(item)">Delete</a>
        </div>
      </div>
    </div>
    <div v-else>
      <p class="fst-italic">Belum ada task</p>
    </div>
  </div>
  <div class="action py-2 col-8" style="margin-left: 10px;">
    <a href="#" class="add-button" v-if="!isCreating" @click="isCreating = !isCreating">Add
      Task</a>
    <div class="add-card" v-else>
      <div v-if="isTitleEmpty" class="error-message btn btn-danger mb-1">Title harus di isi!</div>
      <div class="card mb-2">
        <div class="card-body d-flex flex-column p-0">
          <input v-model="titleValue" class="form-control border-0 mb-2" placeholder="Title" type="text">
          <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description"
            rows="3"></textarea>
        </div>
      </div>
      <div class="button-wrapper d-flex">
        <button @click="addTask" class="btn btn-primary me-2">Save</button>
        <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
      </div>
    </div>
  </div>
</template>


<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  data() {
    return {
      tasks: [
      ],
      isGrid: {
        type: Boolean,
        required: true,
        default: true
      },
      isCreating: false,
      titleValue: '',
      descriptionValue: '',
      isTitleEmpty: false
    }
  },
  methods: {
    addTask() {
      if (this.titleValue.trim() === '') {
        this.isTitleEmpty = true
      } else {
        console.log('title: ', this.titleValue);
        console.log('description: ', this.descriptionValue);
        this.tasks.push({
          title: this.titleValue,
          description: this.descriptionValue,
          isDone: false
        })
        console.log(this.tasks)

        this.titleValue = '';
        this.descriptionValue = '';
        this.isCreating = false;
        this.isTitleEmpty = false;
      }
    },
    deleteTask(item) {
      const index = this.tasks.findIndex(task => task === item);
      if (index !== -1) {
        this.tasks.splice(index, 1)
      }
    }
  }
}
</script>