<script lang="ts">
	import { variables } from '$lib/env';
	import type { Nutrition } from '$lib/models/Nutrition';
	import axios from 'axios';
	import NutritionLabel from '$lib/components/nutrition/nutrition_label.svelte';
	import NutritionForm from '$lib/components/nutrition/nutrition_form.svelte';

	let upc: string = '';
	let serving_size: number = null;
	let serving_unit: string = '';
	let calories: number = null;
	let total_fat: number = null;
	let saturated_fat: number = null;
	let trans_fat: number = null;
	let cholesterol: number = null;
	let sodium: number = null;
	let total_carbohydrates: number = null;
	let dietary_fiber: number = null;
	let total_sugar: number = null;
	let added_sugar: number = null;
	let protein: number = null;
	let description: string = '';

	let status_message = '';

	let placeholder: Nutrition = {
		upc: '70501635720',
		description: 'Tomato 🍅',
		serving_size: 0,
		serving_unit: 'cups (32g)',
		calories: 0,
		total_fat: 0,
		saturated_fat: 0,
		trans_fat: 0,
		cholesterol: 0,
		sodium: 0,
		total_carbohydrates: 0,
		dietary_fiber: 0,
		total_sugar: 0,
		added_sugar: 0,
		protein: 0
	};

	function resetData() {
		upc = '';
		description = '';
		serving_size = null;
		serving_unit = '';
		calories = null;
		total_fat = null;
		saturated_fat = null;
		trans_fat = null;
		cholesterol = null;
		sodium = null;
		total_carbohydrates = null;
		dietary_fiber = null;
		total_sugar = null;
		added_sugar = null;
		protein = null;

		status_message = '';
	}

	function handleSubmit() {
		let nutrition: Nutrition = {};
		let canPost: boolean = false;

		if (upc) {
			nutrition.upc = upc;
			canPost = true;
		}
		if (description) {
			nutrition['description'] = description;
			canPost = true;
		}
		if (serving_size) {
			nutrition['serving_size'] = serving_size;
			canPost = true;
		}
		if (serving_unit) {
			nutrition['serving_unit'] = serving_unit;
			canPost = true;
		}
		if (calories) {
			nutrition['calories'] = calories;
			canPost = true;
		}
		if (total_fat) {
			nutrition['total_fat'] = total_fat;
			canPost = true;
		}
		if (saturated_fat) {
			nutrition['saturated_fat'] = saturated_fat;
			canPost = true;
		}
		if (trans_fat) {
			nutrition['trans_fat'] = trans_fat;
			canPost = true;
		}
		if (cholesterol) {
			nutrition['cholesterol'] = cholesterol;
			canPost = true;
		}
		if (sodium) {
			nutrition['sodium'] = sodium;
			canPost = true;
		}
		if (total_carbohydrates) {
			nutrition['total_carbohydrates'] = total_carbohydrates;
			canPost = true;
		}
		if (dietary_fiber) {
			nutrition['dietary_fiber'] = dietary_fiber;
			canPost = true;
		}
		if (total_sugar) {
			nutrition['total_sugar'] = total_sugar;
			canPost = true;
		}
		if (added_sugar) {
			nutrition['added_sugar'] = added_sugar;
			canPost = true;
		}
		if (protein) {
			nutrition['protein'] = protein;
			canPost = true;
		}

		// Make Description Mandatory
		if (!description) {
			canPost = false;
		}

		if (canPost) {
			axios
				.post(variables.SERVER_URL + '/nutrition', nutrition)
				.then((response) => {
					alert('Nutrition Information Added!');
					resetData();
				})
				.catch((error) => {
					console.log(error);
					alert(error);
				});
		} else {
			status_message = 'Please complete the above form!';
		}
	}
</script>

<div>
	<h2 class="text-2xl m-4">Add Nutrition Information</h2>
	<NutritionForm
		bind:description
		bind:serving_size
		bind:serving_unit
		bind:calories
		bind:total_fat
		bind:saturated_fat
		bind:trans_fat
		bind:cholesterol
		bind:sodium
		bind:total_carbohydrates
		bind:dietary_fiber
		bind:total_sugar
		bind:added_sugar
		bind:protein
		bind:placeholder
		bind:upc
		bind:status_message
		{handleSubmit}
		button_text="Add Nutrition Data"
	/>

	<div class="w-full max-w-lg mx-4 flex justify-center items-center">
		<NutritionLabel
			{description}
			{serving_size}
			{serving_unit}
			{calories}
			{total_fat}
			{saturated_fat}
			{trans_fat}
			{cholesterol}
			{sodium}
			{total_carbohydrates}
			{dietary_fiber}
			{total_sugar}
			{added_sugar}
			{protein}
			{placeholder}
		/>
	</div>
</div>
