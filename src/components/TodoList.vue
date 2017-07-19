<template>
	<div id="todoListContainer">
		<div class="new-todo" v-bind:class="{'active': searchActive}">
			<icon name="check"></icon>
			<input type="text" name="newTodo" placeholder="What do you need to do?" @focus="searchActive = true" @blur="searchActive = false">
		</div>
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
			searchActive: false,
			todos: [
				{
					done: false,
					title: 'Test TODO'
				},
				{
					done: true,
					title: 'Test TODO'
				},
				{
					done: true,
					title: 'Test TODO'
				},
				{
					done: false,
					title: 'Test TODO'
				},
				{
					done: false,
					title: 'Test TODO'
				}
			]
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

	hr {
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
}
</style>
