<template>
	<form class="form--body" @submit="submitHandler">
		<h2>New Todo Item</h2>
		<div class="form--control">
			<label for="agenda">Your agenda</label>
			<input
				required
				type="text"
				name="agenda"
				class="form--input"
				v-model="agenda"
				placeholder="Go to the market"
				@input="validate"
			/>
		</div>
		<div class="form--control">
			<label for="deadline">Deadline</label>
			<input
				required
				type="text"
				name="deadline"
				class="form--input"
				v-model="deadline"
				placeholder="20th Oct. 2021"
				@input="validate"
				autocomplete="false"
			/>
		</div>

		<div class="form--button-group">
			<Button
				:btn="{
					type: 'button',
					content: 'Cancel',
					classes: ['md', 'form--button', 'cancel'],
					clickHandler: toggleForm,
				}"
			/>

			<input
				:disabled="isSubmitDisabled"
				type="submit"
				class="button md primary"
				value="Add Item"
			/>
		</div>
	</form>
</template>

<script>
import Button from "../UI/Button.vue";

export default {
	data() {
		return {
			agenda: "",
			deadline: "",
			isSubmitDisabled: true,
		};
	},

	name: "NewItemForm",
	props: {
		toggleForm: Function,
	},
	components: {
		Button,
	},
	methods: {
		clearForm() {
			this.agenda = "";
			this.deadline = "";
		},

		validate() {
			if (this.agenda.length > 0 && this.deadline.length > 0)
				this.isSubmitDisabled = false;
			else this.isSubmitDisabled = true;
		},

		submitHandler(event) {
			event.preventDefault();
			this.toggleForm();
			this.$emit("add-item", {
				agenda: this.agenda,
				deadline: this.deadline,
			});
			this.clearForm();
		},
	},
};
</script>

<style></style>