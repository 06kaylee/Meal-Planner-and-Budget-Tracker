<template>
	<form class="add-goal-form" @submit.prevent="submitForm">
		<div class="form-control title">
			<label for="title" id="title-label">Title</label>
			<input type="text" id="title" v-model="title" />
		</div>

		<div class="form-control category">
			<h3 id="category-title">Category</h3>
			<input
				type="radio"
				id="fitness"
				name="category"
				value="fitness"
				v-model="category"
			/>
			<label for="fitness">Fitness</label>

			<input
				type="radio"
				id="nutrition"
				name="category"
				value="nutrition"
				v-model="category"
			/>
			<label for="nutrition">Nutrition</label>

			<input
				type="radio"
				id="other"
				name="category"
				value="other"
				v-model="category"
			/>
			<label for="other">Other</label>
		</div>

		<div class="form-control date">
			<label for="start-date" id="start-date-label">Start Date</label>
			<input
				type="date"
				id="start-date"
				name="start-date"
				v-model="startDate"
			/>

			<label for="end-date" id="end-date-label">End Date</label>
			<input type="date" id="end-date" name="end-date" v-model="endDate" />
		</div>

		<input type="submit" />
	</form>
</template>

<script>
import GoalService from "../../services/GoalService";

export default {
	data() {
		return {
			title: "",
			category: "",
			startDate: "",
			endDate: "",
		};
	},
	methods: {
		async submitForm() {
			const newGoal = {
				title: this.title,
				category: this.category,
				startDate: this.startDate,
				endDate: this.endDate,
			};

			await GoalService.add(newGoal);
			this.$router.replace("/goals");
		},
	},
};
</script>

<style scoped>
.add-goal-form {
	padding-top: 0.6rem;
}

input {
	padding: 0.4rem;
	border-radius: 0.2rem;
	border: 1px solid black;
}

#category-title {
	font-size: 1rem;
	padding-bottom: 0.3rem;
}

.form-control {
	margin-bottom: 1rem;
}

.category label {
	padding: 0 1.5rem 0 0.3rem;
}

.date {
	display: grid;
	grid-template-areas:
		"start end"
		"start-date end-date";
	column-gap: 2rem;
}

#title-label,
#start-date-label,
#end-date-label {
	display: block;
	font-weight: bold;
	padding-bottom: 0.3rem;
}

#start-date-label {
	grid-area: start;
}

#end-date-label {
	grid-area: end;
}

#start-date {
	grid-area: start-date;
}

#end-date {
	grid-area: end-date;
}
</style>
