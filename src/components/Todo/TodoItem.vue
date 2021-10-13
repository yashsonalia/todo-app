<template>
	<div class="todo--item-inner">
		<div class="todo--item-checkbox">
			<input
				class="item--checkbox"
				type="checkbox"
				:name="'checkbox' + item.id"
				:id="'checkbox' + item.id"
				:checked="item.isComplete"
				@click="$emit('toggle-item', item.id)"
			/>
			<label :for="'checkbox' + item.id">
				<span :class="item.isComplete ? 'checked' : ''"></span>
			</label>
		</div>
		<div class="todo--item-text">
			<h3>{{ item.agenda }}</h3>
			<p>
				Ends: <span>{{ item.deadline }}</span>
			</p>
		</div>
		<div class="todo--item-options" @click="$emit('delete-item', item.id)">
			<span></span>
		</div>
	</div>
</template>
<script>
export default {
	name: "TodoItem",
	props: {
		item: Object,
	},
};
</script>