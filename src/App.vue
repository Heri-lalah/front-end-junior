<template>
  <Navbar/>
  <div class="container-fluid">
    <div class="mt-3">
      <div class="row">
        <div class="col"></div>
        <div class="col-8">
          <div class="row g-2 align-items-center">
            <div class="col-sm-12 col-md-4">
              <h3>Tasks</h3>
            </div>
            <div class="col-sm-12 col-lg-6">
              <section v-show="notCompletedCount>0">
                <span class="fw-bold">Unfinished task</span> <span class="badge fw-bold bg-warning text-danger">{{ notCompletedCount }}</span>
              </section>
            </div>
            <div class="col-sm-12 col-lg-2">
              <button
              class="btn btn-primary btn-sm"
              data-bs-toggle="modal"
              data-bs-target="#modalTask"
              @click.prevent="resetForm"
              >New task</button>
            </div>
          </div>

          <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Title</th>
                <th scope="col">Description</th>
                <th scope="col">Status</th>
                <th scope="col">Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="task in taskList">
                <th scope="row">{{ task.id }}</th>
                <td>{{ task.title }}</td>
                <td>{{ task.description }}</td>
                <td>
                  <div class="form-check form-switch">
                    <input class="form-check-input" v-on:change="setCompleted(task)" :checked="task.completed" type="checkbox" role="switch"  :id="'task' + task.id">
                    <label class="form-check-label" for="flexSwitchCheckDefault">Completed</label>
                  </div>
                </td>
                <td>
                  <div class="row g-1">
                    <div class="col"><button class="d-block w-100 btn btn-primary" @click.prevent="setModalValue(task)" data-bs-toggle="modal" data-bs-target="#modalTask">Edit</button></div>
                    <div class="col"><button class="d-block w-100 btn btn-success" @click.prevent="setCompleted(task)">Completed</button></div>
                    <div class="col"><button class="d-block w-100 btn btn-danger" @click.prevent="onDelete(task)">Delete</button></div>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="col"></div>
      </div>
    </div>
    <div class="modal fade" id="modalTask" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="taskTitle"> {{ isEditing? 'Edit' : 'New task' }} </h1>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form id="taskForm">
              <div class="mb-3">
                <label for="inputTitle" class="form-label">Title</label>
                <input type="text"
                v-model="form.title"
                class="form-control"
                id="inputTitle"
                placeholder="Title..."
                @input="$emit('update:title', $event.target.value)"
                >
              </div>
              <div class="mb-3">
                <label for="inputDescription" class="form-label">Description</label>
                <textarea class="form-control"
                placeholder="Enter the description of the new task here ..."
                id="inputDescription"
                rows="3"
                v-model="form.description"
                ></textarea>
              </div>
              <div v-show="isEditing" class="form-check form-switch">
                <input class="form-check-input"
                v-model="form.completed"
                :checked="form.completed"

                type="checkbox"
                role="switch"
                >
                <label class="form-check-label" for="flexSwitchCheckDefault">Completed</label>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" id="closeModal" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>

            <button v-show="!isEditing" type="submit" v-if="validationForm" form="taskForm"  @click="onSubmit"
            class="btn btn-primary"
            >Add</button>

            <button v-show="isEditing" type="submit" v-if="validationForm" form="taskForm"  @click.prevent="onEdit"
            class="btn btn-primary"
            >Edit</button>
          </div>
        </div>
      </div>
    </div>
</div>
</template>
<script setup>
import Navbar from '@/components/Navbar.vue';
import { reactive, computed, ref, onMounted } from 'vue';
const taskList =reactive([
  {
    id: 1,
    title : "Add logo",
    description: "The description of add logo",
    completed : true
  },
  {
    id:2,
    title : "Add navbar",
    description: "The description of add navbar",
    completed : false
  },
  {
    id:3,
    title : "Add new task",
    description: "The description of add new task",
    completed : false
  }
]);

const notCompletedCount = ref(null);

const lastId = computed(() => {
   return taskList.length;
})
const isEditing = ref(false);

const validationForm = computed(() => {
  if(form.id!= "" || form.description!="")
  {
    return true
  }
  return false
})
const closeModal = () => {
  resetForm();
  return document.getElementById("closeModal").click();
}
const form = reactive({
  id: "",
  title: "",
  description:"",
  completed: false,
  validation: validationForm
})
const resetForm = () => {
  form.id = "";
  form.title = "";
  form.description = "";
  form.completed = false;
}

const getCount = () => {
  const count = taskList.filter((child) => child.completed == false);
  return notCompletedCount.value = count.length;
}

const setCompletedCount = () => {
  notCompletedCount.value = getCount();
}

onMounted(() => {
  getCount();
});

const setCompleted = (value) => {
  const index = taskList.findIndex((child) => child.id == value.id);
  if(index!==null || index==undefined) {
    taskList[index].completed = !taskList[index].completed;
    setCompletedCount();
  }
}
const onSubmit = (e) => {
	e.preventDefault();

  taskList.push({
    id: lastId.value + 1,
    title: form.title,
    description : form.description,
    completed: form.completed,
  });
  setCompletedCount();
  closeModal();
}
const onEdit = () => {
  const index = taskList.findIndex((index) => index.id == form.id);
  if(index!==null || index==undefined) {
    taskList[index].title = form.title;
    taskList[index].description = form.description;
    taskList[index].completed = form.completed;
  }
  setCompletedCount();
  closeModal();
}

const onDelete = (key) => {
  const index = taskList.findIndex((index) => index.id == key.id);
  taskList.pop(taskList[index]);
  setCompletedCount();
}
const setModalValue = (value) => {
  isEditing.value = true
  form.id = value.id;
  form.title = value.title;
  form.description = value.description;
  form.completed = value.completed;
}
</script>