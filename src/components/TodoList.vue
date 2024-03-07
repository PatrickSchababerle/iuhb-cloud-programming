<template>
	<div class="input-group add-entry mb-5">
		<input class="form-control" ref="todoinput" placeholder="Add a new entry...">
		<button class="add-button" @click="this.addTodo()">
			<svg fill="currentColor" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 36 36">
				<path id="_art" class="st1" d="M25.5,16.5l-5.9,0l0-5.9C19.6,9.7,18.9,9,18,9c-0.9,0-1.5,0.7-1.5,1.5l0,5.9l-5.9,0h0
								  C9.7,16.4,9,17.1,9,18c0,0.9,0.7,1.5,1.5,1.5l5.9,0l0,5.9c0,0.9,0.7,1.5,1.5,1.5c0.9,0,1.5-0.7,1.5-1.5l0-5.9l5.9,0h0
								  c0.9,0,1.5-0.7,1.5-1.5C27,17.2,26.3,16.5,25.5,16.5L25.5,16.5z"></path>
			</svg>
		</button>
	</div>
	<div class="mb-5 px-3" v-if="todos.length">
		<h2 class="my-5">
			Open
		</h2>
		<div class="row" v-for="(todo, index) in todos" :key="index">
			<TodoElement :todo="todo" v-if="!todo.status" />
		</div>
		<span v-if="hasNoOpenTodos">
			Excellent, you've done a great job!
		</span>
		<h2 class="my-5">
			Done
		</h2>
		<div class="row" v-for="(todo, index) in todos" :key="index">
			<TodoElement :todo="todo" v-if="todo.status" />
		</div>
		<span v-if="hasNoFinishedTodos">
			Uff, there is a lot to do... Start checking items from above!
		</span>
	</div>
</template>

<script>
import TodoElement from "@/components/TodoElement.vue";
import { Modal } from 'bootstrap';

export default {
	name: 'TodoList',
	components: {
		TodoElement
	},
	data() {
		return {
			todos: []
		}
	},
	computed: {

		hasNoOpenTodos() {
			return this.todos.filter((todo) => { return !todo.status }).length === 0;
		},

		hasNoFinishedTodos() {
			return this.todos.filter((todo) => { return todo.status }).length === 0;
		}

	},
	mounted() {

		this.showDisclaimer();

		let loaded = localStorage.getItem(
			'todos'
		);

		if(loaded) {
			this.todos = JSON.parse(loaded);
		}

	},
	methods: {

		showDisclaimer() {
			let isConfirmed = localStorage.getItem('disclaimer_confirmed');
			if(!isConfirmed) {
				let disclaimer = new Modal(document.getElementById('disclaimer'), null);
				disclaimer.show();
			}
		},

		addTodo() {

			let value = this.$refs.todoinput.value;

			this.todos.push({
				title: value,
				status: false
			});

			this.storeLocal();

			this.$refs.todoinput.value = "";

		},

		removeTodo(index) {
			this.todos.splice(index, 1);
			this.storeLocal();
		},

		storeLocal() {
			localStorage.setItem(
				'todos', JSON.stringify(this.todos)
			)
		}

	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h3 {
		margin: 40px 0 0;
	}
	ul {
		list-style-type: none;
		padding: 0;
	}
	li {
		display: inline-block;
		margin: 0 10px;
	}
	a {
		color: #42b983;
	}
	.add-entry input {
		background-color: var(--element-background-color);
		border: none;
		height: 60px;
		border-radius: 50px !important;
		font-size: 30px;
		color: white;
		font-weight: bold;
		padding-left: 35px;
		padding-right: 70px;
	}
	.add-entry input::placeholder {
		color: var(--deactivated-text);
	}
	.add-button {
		background-color: var(--accent-color);
		border-radius: 50px !important;
		border: none;
		color: white;
		height: 40px;
		justify-content: center;
		position: absolute;
		right: 10px;
		top: 50%;
		transform: translateY(-50%);
		width: 40px;
		z-index: 100;
	}
</style>
