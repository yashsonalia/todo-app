<template>
	<div class="form--control-inner">
		<label :for="field.name">{{ field.label }}</label>
		<input
			:id="field.id"
			:name="field.name"
			:type="field.type"
			:placeholder="field.placeholder"
			:class="['form--input', ...field.classes]"
			:v-model="field.model"
		/>
	</div>
</template>

<script>
export default {
	name: "InputField",
	props: {
		field: Object,
	},
};
</script>

<style></style>