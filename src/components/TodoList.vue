<template>
	<div id="todoListContainer">
		<div class="new-todo" v-bind:class="{'active': searchActive}">
			<icon name="check"></icon>
			<input type="text" name="newTodo" @focus="searchActive = true" @blur="searchActive = false" v-model="newTodoTitle" v-on:keyup.enter="addTodo">
		</div>
		<div class="add-todo-hint" v-bind:class="{'show': newTodoTitle.length > 0}">Press <kbd>Enter</kbd> to add your todo</div>
		<hr>
		<div class="todo-list">
			<div v-for="(todo, i) in sortedTodos.active" :key="i" class="todo-container active">
				<Todo v-bind:todo="todo" class="todo"></Todo>
				<div class="todo-functions">
					<button v-if="!todo.editing" class="todo-function todo-remove" @click="function() {removeTodo(todo.index)}"><icon name="close" scale="0.75"></icon></button>
					<button v-if="!todo.editing" class="todo-function todo-edit" @click="function() {editTodo(todo.index)}"><icon name="pencil" scale="0.75"></icon></button>
					<button v-if="todo.editing" class="todo-function todo-edit" @click="function() {saveTodo(todo.index)}"><icon name="save" scale="0.75"></icon></button>
				</div>
			</div>
			<hr v-if="sortedTodos.done.length > 0 && sortedTodos.active.length > 0">
			<div v-for="(todo, i) in sortedTodos.done" :key="i + sortedTodos.active.length" class="todo-container done">
				<Todo v-bind:todo="todo" class="todo"></Todo>
				<div class="todo-functions">
					<button v-if="!todo.editing" class="todo-function todo-remove" @click="function() {removeTodo(todo.index)}"><icon name="close" scale="0.75"></icon></button>
					<button v-if="!todo.editing" class="todo-function todo-edit" @click="function() {editTodo(todo.index)}"><icon name="pencil" scale="0.75"></icon></button>
					<button v-if="todo.editing" class="todo-function todo-edit" @click="function() {saveTodo(todo.index)}"><icon name="save" scale="0.75"></icon></button>
				</div>
			</div>
			<div class="empty-list" v-if="noTodos">
				<p>
					<icon name="smile-o"></icon> Nothing to do!
				</p>
				<p>
					Add a todo to get started.
				</p>
			</div>
		</div>
		<hr>
		<div class="functions" v-if="!noTodos">
			<span class="function remove-done" @click="removeDone">
				Remove done
			</span>
		</div>
	</div>
</template>

<script>
import Todo from './Todo'

export default {
	name: 'todoList',
	data() {
		return {
			newTodoTitle: '',
			searchActive: false,
			todos: [0, 0, 0, 0, 0].map(function(todo) {
				return {
					title: 'Test TODO',
					done: Math.random() > .5 ? true : false,
					timestamp: new Date('2017-' + (Math.ceil(Math.random() * 2) + 5) + '-' + Math.ceil(Math.random() * 20)),
					editing: false
				}
			})
		}
	},
	methods: {
		addTodo: function() {
			let processedTitle = this.newTodoTitle.trim()
			if (processedTitle.length > 0) {
				this.todos.push({
					done: false,
					title: processedTitle,
					timestamp: new Date(),
					editing: false
				})
			}

			this.newTodoTitle = ''
		},
		editTodo: function(i) {
			this.todos[i].editing = true;
		},
		saveTodo: function(i) {
			this.todos[i].editing = false;
		},
		removeTodo: function(i) {
			this.todos.splice(i, 1)
		},
		removeDone: function() {
			this.todos = this.todos.filter(function(todo) {
				return !todo.done
			})
		}
	},
	computed: {
		noTodos: function() {
			return this.todos.length <= 0
		},
		sortedTodos: function() {
			let active = []
			let done = []
			this.todos.forEach(function(todo, i) {
				todo.index = i
				todo.done ? done.push(todo) : active.push(todo)
			})

			active.sort(function(a, b) {
				return a.timestamp.getTime() < b.timestamp.getTime()
			})
			done.sort(function(a, b) {
				return a.timestamp.getTime() < b.timestamp.getTime()
			})

			return {
				active: active,
				done: done
			}
		}
	},
	components: {
		Todo: Todo
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../assets/scss/variables';

#todoListContainer {
	margin: 2rem;

	background: rgba(#fff, .8);

	border-radius: 1rem;

	overflow: hidden;

	hr {
		margin: 0;

		border: none;
		border-top: 1px solid rgba(#444, .2);
	}

	.new-todo {
		display: flex;
		align-items: center;

		margin: 1rem;
		padding: .25rem 1rem;

		background: rgba(#444, .1);

		border: none;
		border-radius: 999px;

		transition: .3s all;

		color: #444;

		&.active {
			background: rgba(#fff, .9);
			outline: none;
		}

		input[type=text] {
			flex-grow: 1;
			padding-left: .5rem;

			color: inherit;

			font-family: inherit;
			font-size: 1.25rem;

			background: transparent;
			border: none;

			&:focus, &:active {
				outline: none;
			}
		}
	}

	.add-todo-hint {
		margin: 0 1rem;
		height: 0;

		font-size: .8em;
		color: rgba(#444, .8);

		overflow: hidden;

		transition: .3s all;

		&.show {
			margin-bottom: 1rem;
			padding: .3em 0;
			height: 1em;
		}

		kbd {
			padding: .1em;

			border: 1px solid rgba(#444, .2);
			border-radius: 4px;
		}
	}

	.todo-list {
		display: flex;
		flex-direction: column;

		.todo-container {
			display: flex;

			&.active {
				//
			}

			&.done {
				background: $success;
			}

			&:hover {
				.todo-functions {
					padding: .5rem;
					right: 0;
					opacity: 1;
				}
			}

			.todo {
				flex-grow: 1;
			}

			.todo-functions {
				display: flex;
				position: relative;
				padding: .5rem;
				right: -200px;

				transition: .3s all;

				.todo-function {

					color: #444;

					background: transparent;

					border: none;

					cursor: pointer;

					overflow: hidden;

					transition: .3s all;

					&:focus, &:active {
						outline: none;
					}
				}
			}
		}

		.empty-list {
			padding: 1rem;
			color: rgba(#444, .5);
			text-align: center;
		}
	}

	.functions {
		padding: .25rem 1rem;

		-webkit-user-select: none;
		-moz-user-select: none;
		-ms-user-select: none;
		user-select: none;

		.function {
			font-size: .7rem;
			color: rgba(#444, .7);

			transition: .3s all;

			cursor: pointer;

			&:hover {
				color: rgba(#444, 1);
			}
		}
	}
}
</style>
