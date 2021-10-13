<template>
	<button
		:type="btn.type"
		:class="['button', ...btn.classes]"
		@click="btn.clickHandler()"
	>
		{{ btn.content }}
	</button>
</template>

<script>
export default {
	name: "Button",
	props: {
		btn: Object,
	},
};
</script>