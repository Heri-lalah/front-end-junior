<template>
  <Navbar/>
  <div class="container-fluid">
    <div class="mt-3">
      <div class="row">
        <div class="col-6">
          <p>{{ form.title }}</p>
          <p>{{ form.description }}</p>
        </div>
        <div class="col"></div>
      </div>
    </div>
    <AddTaskModal v-model:title="form.title" :description="form.description"/>
  </div>
</template>
<script setup>
import Navbar from '@/components/Navbar.vue';
import AddTaskModal from '@/components/AddTaskModal.vue';
import { reactive } from 'vue';
const form = reactive({
  title: "A",
  description:"",
})
</script>