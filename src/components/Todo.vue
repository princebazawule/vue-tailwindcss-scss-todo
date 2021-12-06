<template>
	<div class="list flex flex-col justify-center text-2xl">
		<div class="form mb-12 relative">
			<form @submit.prevent="addTodo()">
				<input
					ref="input"
					type="text"
					placeholder="Enter new item"
					class="bg-gray-100 py-4 pl-4 pr-20"
					v-model="newTodo"
				/>
				<span class="absolute right-40 top-1/2 transform -translate-y-1/2 italic text-gray-400"
					>{{ todos.length }}/5</span
				>
				<button class="bg-purple-700 hover:bg-purple-800 p-4 text-white font-bold w-36 transition duration-200">
					Add
				</button>
			</form>
		</div>
		<div v-if="todos.length" class="list">
			<div
				v-for="(todo, index) in todos"
				:key="todo"
				class="py-2 text-gray-900 flex flex-row flex-nowrap justify-between"
			>
				<p @click="doneTodo(todo)" class="flex-grow text-left relative group" :class="{ done: todo.done }">
					{{ todo.content }}
					<span class="absolute top-1/2 transform -translate-y-1/2 right-4 p-2 bg-gray-300 rounded-md text-sm opacity-0 group-hover:opacity-100">✔</span>
				</p>
				<button
					title="delete"
					@click="removeTodo(index)"
					class="hover:text-gray-400 transition duration-200 transform-gpu scale-75 hover:scale-100"
				>
					✕
				</button>
			</div>
		</div>
		<div v-else class="list">
			<p class="text-4xl font-light">Go on, add some items!</p>
		</div>
	</div>
</template>

<script>
import { ref } from 'vue'
export default {
	name: 'Todo',
	setup() {
		const maxTodos = 5
		const input = ref({})
		const newTodo = ref('')
		const todosData = JSON.parse(localStorage.getItem('todos')) || []
		const todos = ref(todosData)
		const addTodo = () => {
			trackTodosLength()
			if (todos.value.length < maxTodos) {
				if (newTodo.value) {
					if (todos.value.length <= maxTodos) {
						todos.value.push({
							done: false,
							content: newTodo.value,
						})
					}
				}
				newTodo.value = ''
				saveData()
			}
		}
		const doneTodo = (todo) => {
			todo.done = !todo.done
			saveData()
		}
		const removeTodo = (index) => {
			todos.value.splice(index, 1)
			saveData()
		}
		const saveData = () => {
			const storageData = JSON.stringify(todos.value)
			console.log(todos.value.length)
			localStorage.setItem('todos', storageData)
			trackTodosLength()
		}
		const trackTodosLength = () => {
			if (todosData.length >= maxTodos) {
				input.value.disabled = true
			} else {
				input.value.disabled = false
			}
		}

		return { todos, newTodo, addTodo, doneTodo, removeTodo, saveData, input, trackTodosLength }
	},
}
</script>

<style scoped>
.done {
	@apply text-gray-400;
	@apply line-through;
}
</style>
