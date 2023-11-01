

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
					<div class="mb-3">
						<label for="inputTitle" class="form-label">Title</label>
						<input type="email"
						:value="title"
						class="form-control"
						id="inputTitle"
						placeholder="Title..."
						@input="$emit('update:titles', $event.target.value)"

						>
					</div>
					<div class="mb-3">
						<label for="inputDescription" class="form-label">Description</label>
						<textarea class="form-control"
						placeholder="Enter the description of the new task here ..."
						id="inputDescription"
						rows="3"
						:value="description"
						@input="$emit('update:description', $event.target.value)"
						></textarea>
					</div>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
					<button type="button" class="btn btn-primary">Add</button>
				</div>
			</div>
		</div>
	</div>
</template>
<script setup>
defineProps(['title', 'description'])
defineEmits(['update:title', 'update:description'])

</script>