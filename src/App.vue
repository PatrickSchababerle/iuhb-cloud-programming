<template>
	<h1 class="mb-5">
		Simple Todo App
	</h1>
	<div class="container">
  		<TodoList />
	</div>
	<DisclaimerModal />
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import DisclaimerModal from "@/components/DisclaimerModal.vue";

export default {
  name: 'App',
  components: {
	  DisclaimerModal,
	  TodoList
  }
}
</script>

<style>
	:root {
		--background-color: #101010;
		--element-background-color: rgb(66 66 69/70%);
		--inner-glow-color: rgb(232 232 237 / 11%);
		--text-color: rgb(245, 245, 247);
		--accent-color: #0071e3;
		--deactivated-text: #86868b;
	}
	body {
		background-color: var(--background-color) !important;
	}
	#app {
		font-family: SF Pro Display, SF Pro Icons, Helvetica Neue, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: white;
		margin-top: 60px;
	}
	h1 {
		font-size: 56px;
		line-height: 1.0714285714;
		font-weight: 600;
		letter-spacing: -0.005em;
		font-family: SF Pro Display, SF Pro Icons, Helvetica Neue, Helvetica, Arial, sans-serif;
	}
</style>
