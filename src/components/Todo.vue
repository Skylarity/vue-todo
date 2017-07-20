<template lang="html">
	<div class="todo" v-bind:class="{'done': todo.done, 'warning': status === 'warning', 'danger': status === 'danger'}">
		<label class="todo-checkbox">
			<input type="checkbox" name="done" v-model="todo.done">
			<div class="check"><icon name="check"></icon></div>
		</label>
		<div class="todo-info">
			<div class="title"><icon name="exclamation-triangle" scale=".75" v-if="status === 'danger'"></icon>{{ todo.title }}</div>
			<div class="date">added {{ todoDate }}</div>
		</div>
	</div>
</template>

<script>
import moment from 'moment'

export default {
	name: 'todo',
	props: ['todo'],
	computed: {
		todoDate: function() {
			return moment(this.todo.timestamp, 'YYYYMMDD').fromNow()
		},
		status: function() {
			if (!this.todo.done) {
				let current = new Date()
				current = current.getTime()
				let stamp = this.todo.timestamp.getTime()
				let week = (1000 * 60 * 24 * 7)
				let month = (1000 * 60 * 24 * 7 * 4)

				// TODO: Use moment
				if (current - stamp > month) {
					return 'danger'
				} else if (current - stamp > week) {
					return 'warning'
				}
			}
		}
	}
}
</script>

<style scoped lang="scss">

$success: #81c784;
$warning: #fdd835;
$danger: #e53935;

.todo {
	display: flex;

	padding: 1rem 2rem .5rem;

	transition: .3s all;

	&.done {
		.title {
			text-decoration: line-through;
		}

		background: $success;
	}

	&.warning {
		background: $warning;
	}

	&.danger {
		color: #fff;
		background: $danger;

		.date {
			color: #fff !important;
		}
	}

	&:last-child {
		padding-bottom: 1rem;
	}

	input[type=checkbox] {
		//
	}

	.todo-info {
		margin-left: .5rem;

		.title {
			flex-grow: 1;

			.fa-icon {
				margin-right: .25rem;
			}
		}

		.date {
			font-size: .75em;
			color: rgba(#444, .6);
		}
	}

	.todo-checkbox {
		input {
			display: none;
		}

		.check {
			position: relative;
			width: 20px;
			height: 20px;
			border-radius: 50%;
			border: 4px solid rgba(#444, .2);
			box-sizing: border-box;
			transition: all 0.3s;
			cursor: pointer;
		}

		input:checked + .check {
			border: 10px solid rgba(#fff, .9);
		}

		.check .fa-icon {
			color: transparent;
			transition: all 0.3s;
		}

		input:checked + .check .fa-icon {
			color: $success;
			top: -7px;
			left: -8px;
		}

		.fa-icon {
			position: absolute;
			top: -1px;
			left: -2px;
		}
	}
}
</style>
