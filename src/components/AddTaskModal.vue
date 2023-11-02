

<template>
	<!-- Modal -->
	<div class="modal fade" id="add-new-task" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="add-new-task">New task</h1>
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

							@input="$emit('update:description', $event.target.value)"
							></textarea>
						</div>
					</form>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
					<button type="submit" form="taskForm"  @click="onSubmit"  class="btn btn-primary">Add</button>
				</div>
			</div>
		</div>
	</div>
</template>
<script setup>
import { reactive } from "vue";
defineProps(['title', 'description'])
defineEmits(['update:title', 'update:description'])
const form = reactive({
	title : "",
	description : "",
})
const onSubmit = (e) => {
	e.preventDefault();
	console.log(form)
}
</script>