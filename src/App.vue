<template>
<div class="min-h-screen border-8 border-gray-900 flex flex-col justify-center items-center">
	<Todo />
</div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
	name: 'App',
	components: { Todo },
	data() {
		return {}
	},
	methods: {},
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}
</style>
