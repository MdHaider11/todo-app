<template>
	<div id="app">
		<div class="ui-form">
			<div v-if="isEdit">
				<form @submit.prevent="itemUpdate">
					<input type="text" placeholder="Edit Item" v-model="todo" />
					<input type="submit" value="Update" />
				</form>
			</div>
			<div v-else>
				<form @submit.prevent="itemSubmit">
					<input type="text" placeholder="Add Item" v-model="todo" />
					<input type="submit" value="+" />
				</form>
			</div>
			<ul>
				<li v-for="(todo, index) in todos" :key="index">
					{{ todo }}
					<span
						>(
						<a
							href="javascript:void(0)"
							@click="editItem(todo, index)"
							>Edit</a
						>
						||
						<a href="javascript:void(0)" @click="deleteItem(index)"
							>Delete</a
						>)</span
					>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'App',
		data() {
			return {
				isEdit: false,
				updateIndex: Number,
				todo: '',
				todos: ['Apple', 'Orange', 'Pineapple'],
			};
		},
		methods: {
			itemSubmit() {
				if (this.todo !== '') {
					this.todos.push(this.todo);
					this.todo = '';
				}
			},

			editItem(todo, index) {
				this.isEdit = true;
				this.todo = todo;
				this.updateIndex = index;
			},

			itemUpdate() {
				this.isEdit = false;
				this.todos.splice(this.updateIndex, 1, this.todo);
				this.todo = '';
			},

			deleteItem(index) {
				this.todos.splice(index, 1);
			},
		},
	};
</script>

<style>
	.ui-form input[type='text'] {
		height: 34px;
		padding: 0px 14px;
	}

	.ui-form input[type='submit'] {
		appearance: push-button;
		height: 38px;
		width: auto;
		margin-left: 8px;
		cursor: pointer;
	}

	.ui-form ul {
		list-style-type: auto;
	}
</style>
