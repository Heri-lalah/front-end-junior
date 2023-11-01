<template>
	<nav class="navbar bg-primary navbar-expand-lg">
		<div class="container-fluid">
			<a href="#" class="navbar-brand">Todo-list app</a>
			<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
				<span class="navbar-toggler-icon"></span>
			</button>

			<div class="collapse navbar-collapse" id="navbarSupportedContent">
				<div class="navbar-nav me-auto mb-2 mt-2 mt-lg-0 mb-lg-0">
					<Button class="btn btn-outline-light btn-sm"
					data-bs-toggle="modal"
					data-bs-target="#add-new-task"
					>New task</Button>
				</div>
			</div>
		</div>
	</nav>
</template>