<template>
	<div class="container-fluid" v-cloak>
		<div class="form--container" v-if="isFormVisible">
			<NewItemForm :toggleForm="toggleForm" @add-item="createItem" />
		</div>
		<div class="row d-flex justify-content-center">
			<div class="col-lg-5 col-md-6 col-sm-10 col-xs-12">
				<div class="addItem--container d-flex justify-content-end">
					<Button
						:btn="{
							classes: ['md', 'primary', 'addItem--button'],
							content: 'New Item',
							clickHandler: toggleForm,
						}"
					/>
				</div>
			</div>
		</div>
		<div class="row d-flex justify-content-center">
			<div class="col-lg-5 col-md-6 col-sm-10 col-xs-12">
				<h2 class="headline" v-if="localItems.length === 0">
					No new agenda. Add One!
				</h2>
				<div class="todo--container">
					<TodoList
						:items="localItems"
						@delete-item="deleteItem"
						@toggle-item="toggleItem"
					/>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from "axios";

import NewItemForm from "../components/Form/NewItemForm.vue";
import TodoList from "../components/Todo/TodoList.vue";
import Button from "../components/UI/Button.vue";

// import addIcon from "../assets/add.svg#add";
export default {
	name: "Home",
	components: {
		NewItemForm,
		TodoList,
		Button,
	},

	data() {
		return {
			items: [],
			isFormVisible: false,
			localItems: [],
			api: "http://localhost:5000/items",
		};
	},

	methods: {
		async createItem(item) {
			try {
				const itemData = { ...item, isComplete: false };
				const response = await axios.post(`${this.api}`, {
					...itemData,
				});
				const data = response.data;

				this.items = [...this.items, data];
				this.updateLocalStorage();
			} catch (error) {
				console.log(error);
			}
		},

		async toggleItem(id) {
			try {
				const itemToToggle = await this.getItem(id);
				const updateItem = {
					...itemToToggle,
					isComplete: !itemToToggle.isComplete,
				};

				const response = await axios.put(`${this.api}/${id}`, {
					...updateItem,
				});

				const data = await response.data;
				this.items = this.items.map((item) =>
					item.id === id
						? { ...item, isComplete: data.isComplete }
						: item
				);
				this.updateLocalStorage();
			} catch (error) {
				console.log(error);
			}
		},

		async deleteItem(id) {
			try {
				await axios.delete(`${this.api}/${id}`);

				this.items = this.items.filter((item) => item.id !== id);
				this.updateLocalStorage();
			} catch (error) {
				console.log(error);
			}
		},

		async getItems() {
			try {
				const response = await axios.get(`${this.api}`);
				return await response.data;
			} catch (error) {
				console.log(error);
			}
		},

		async getItem(id) {
			try {
				const response = await fetch(`${this.api}/${id}`);
				return await response.json();
			} catch (error) {
				console.log(error);
			}
		},

		toggleForm() {
			this.isFormVisible = !this.isFormVisible;
		},

		updateLocalStorage() {
			localStorage.localItems = JSON.stringify(this.items);
			this.localItems = JSON.parse(localStorage.localItems);
		},
	},

	async created() {
		this.items = await this.getItems();
		this.updateLocalStorage();
	},
};
</script>
