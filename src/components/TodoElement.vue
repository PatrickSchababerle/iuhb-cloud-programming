<template>
	<div class="col-12 card">
		<div class="card-body d-flex">
			<div class="col d-flex align-items-center text-start">
				{{ todo.title }}
			</div>
			<div class="col-auto d-flex gap-3">
				<div class="d-flex justify-content-center align-items-center">
					<input type="checkbox" class="form-check-input" :checked="todo.status" @click="this.toggleElement()">
				</div>
				<div class="d-flex justify-content-center align-items-center" @click="this.removeTodo()">
					<button class="btn btn-danger d-flex align-items-center justify-content-center">x</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "TodoElement",
	props: {
		todo: {
			type: Object
		},
		index: Number
	},
	methods: {

		toggleElement() {
			this.todo.status = !this.todo.status;
			this.$parent.storeLocal();
		},

		removeTodo() {
			this.$parent.removeTodo(
				this.index
			);
		}

	}
}
</script>

<style>
	.card {
		color: white !important;
		margin-top: 5px;
		margin-bottom: 5px;
		background-color: var(--element-background-color) !important;
		font-size: 20px;
		font-weight: bold;
		border-radius: 5px !important;
	}
	.btn-danger {
		height: 30px;
		width: 30px;
	}
	.form-check-input {
		height: 28px !important;
		width: 28px !important;
		margin: 0 !important;
		background-color: var(--deactivated-text) !important;
		border: none !important;
	}
	.form-check-input:checked {
		background-color: var(--accent-color);
	}
</style>