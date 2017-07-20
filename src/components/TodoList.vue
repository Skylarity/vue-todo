<template>
	<div id="todoListContainer">
		<div class="new-todo" v-bind:class="{'active': searchActive}">
			<icon name="check"></icon>
			<input type="text" name="newTodo" @focus="searchActive = true" @blur="searchActive = false" v-model="newTodoTitle" v-on:keyup.enter="addTodo">
		</div>
		<div class="add-todo-hint" v-bind:class="{'show': newTodoTitle.length > 0}">Press <kbd>Enter</kbd> to add your todo</div>
		<hr>
		<div class="todo-list">
			<Todo v-for="(todo, i) in todos" :key="i" v-bind:todo="todo"></Todo>
		</div>
	</div>
</template>

<script>
import Todo from './Todo'

export default {
	name: 'todoList',
	data () {
		return {
			newTodoTitle: '',
			searchActive: false,
			todos: [
				{
					done: false,
					title: 'Test TODO',
					timestamp: new Date('2017-7-19 18:30:34')
				},
				{
					done: true,
					title: 'Test TODO',
					timestamp: new Date('2017-7-1')
				},
				{
					done: false,
					title: 'Test TODO',
					timestamp: new Date('2017-6-1')
				}
			]
		}
	},
	methods: {
		addTodo: function() {
			let processedTitle = this.newTodoTitle.trim()
			if (processedTitle.length > 0) {
				console.log(processedTitle)

				this.todos.push({
					done: false,
					title: processedTitle,
					timestamp: new Date()
				})
			}

			this.newTodoTitle = ''
		}
	},
	components: {
		Todo: Todo
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#todoListContainer {
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
		margin: 0 1rem 1rem;
		height: 0;

		font-size: .8em;
		color: rgba(#444, .8);

		overflow: hidden;

		transition: .3s height;

		&.show {
			padding: .3em 0;
			height: 1em;
		}

		kbd {
			padding: .1em;

			border: 1px solid rgba(#444, .2);
			border-radius: 4px;
		}
	}
}
</style>
