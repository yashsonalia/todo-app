<template>
	<ul class="todo--list">
		<li class="todo--item" v-for="item in items" :key="item.id">
			<TodoItem
				:item="item"
				@delete-item="$emit('delete-item', item.id)"
				@toggle-item="$emit('toggle-item', item.id)"
			/>
		</li>
	</ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
	name: "TodoList",
	components: {
		TodoItem,
	},
	props: { items: Array },
	emits: ["delete-item", "toggle-item"],
};
</script>

