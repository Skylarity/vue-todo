<template lang="html">
	<div class="todo">
		<input type="checkbox" name="done" v-model="todo.done">
		<span class="title">{{ todo.title }}</span>
	</div>
</template>

<script>
export default {
	name: 'todo',
	props: ['todo']
}
</script>

<style scoped lang="scss">
.todo {
	padding: 1rem 2rem .5rem;

	&:last-child {
		padding-bottom: 1rem;
	}

	// https://codepen.io/Skylarity/pen/RGQNQp
}
</style>
