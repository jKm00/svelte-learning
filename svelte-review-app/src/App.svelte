<script lang="ts">
	import type { Option } from './types/Option'
	import type { Review } from './types/Review'
	import ReviewView from './components/ReviewView.svelte'

	// Initializes ratings
	let id = 0
	const options: Option[] = [
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		},
		{
			id: (id++).toString(),
			value: id,
			label: id.toString()
		}
	]

	let reviewId = 0
	let reviews: Review[] = [{ id: reviewId++, rating: 10, feedback: 'Just a test' }]
	let selected: number
	let feedback: string

	$: reviewCount = reviews.length
	$: average = Math.round(reviews.reduce((subtotal, review) => subtotal + review.rating, 0) / reviews.length * 100) / 100

	function handleSubmit(): void {
		if (selected === undefined) return
		reviews = [{ id: reviewId++, rating: selected, feedback }, ...reviews]
		feedback = ''
	}

	function removeReview(event: CustomEvent): void {
		const review = event.detail
		reviews = reviews.filter(r => r !== review)
	}
</script>

<main>
	<form on:submit|preventDefault={handleSubmit} class="box">
		<fieldset>
			<legend>How would you rate your service with us?</legend>
			<div class="radio-wrapper">
				{#each options as option}
					<input id={option.id} bind:group={selected} type="radio" value={option.value} name="rating" />
					<label for={option.id}>{option.label}</label>
				{/each}
			</div>
			<div class="feedback-wrapper">
				<input bind:value={feedback} type="text" placeholder="Tell us something that keeps you comming back">
				<button class="submit" type="submit" disabled={feedback ? feedback.length < 10 : true}>Send</button>
			</div>
		</fieldset>
	</form>
	<div class="stats">
		<p>{reviewCount} Reviews</p>
		<p>{average ? 'Ratings Average: ' + average : 'No ratings'}</p>
	</div>
	<div class="review-wrapper">
		{#each reviews as review (review.id)}
			<ReviewView review={review} on:remove={removeReview} />
		{/each}
	</div>
</main>

<style>
	main {
		max-width: 50rem;
		margin: auto;
		padding: 2rem 0;
	}

	form {
		background-color: #fff;
		padding: 2rem;
	}

	legend {
		text-align: center;
		font-weight: bold;
		font-size: 1.5rem;
		max-width: 25rem;
		margin-bottom: 1rem;
	}

	.radio-wrapper {
		display: flex;
		justify-content: space-between;
		margin-bottom: 2rem;
	}

	label {
		--size: 3rem;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #eee;
		height: var(--size);
		width: var(--size);
		border-radius: 100vh;
	}

	label:hover {
		background-color: #FFB6C1;
	}

	input[type="radio"]:checked + label {
		background-color: #FF69B4;
		color: #fff;
	}

	input[type="radio"] {
		display: none;
	}

	.feedback-wrapper {
		position: relative;
	}

	.feedback-wrapper input {
		width: 100%;
		padding: 0.75rem;
		border-radius: 0.5rem;
		border: 1px solid #aaa;
	}

	.feedback-wrapper button {
		position: absolute;
		right: 0.5rem;
		top:50%;
		transform: translateY(-50%);
		background-color: #111;
		color: #fff;
		padding: 0.5rem 1.5rem;
		border-radius: 0.5rem;
	}

	.stats {
		display: flex;
		justify-content: space-between;
		color: #fff;
		font-weight: bold;
		margin: 1rem 0;
	}

	.review-wrapper {
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
	}
</style>