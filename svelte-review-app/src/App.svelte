<script lang="ts">
	import type { Option } from './types/Option'
	import type { Review } from './types/Review'

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
	let reviews: Review[] = []
	let selected: number
	let feedback: string

	$: reviewCount = reviews.length
	$: average = reviews.reduce((subtotal, review) => subtotal + review.rating, 0) / reviews.length

	function handleSubmit(): void {
		if (selected === undefined) return
		reviews = [...reviews, { id: reviewId++, rating: selected, feedback }]
		feedback = ''
	}

	function removeReview(review: Review): void {
		reviews = reviews.filter(r => r !== review)
	}
</script>

<main>
	<form on:submit|preventDefault={handleSubmit}>
		<fieldset>
			<legend>How would you rate your service with us?</legend>
			{#each options as option}
				<label for={option.id}>{option.label}</label>
				<input id={option.id} bind:group={selected} type="radio" value={option.value} name="rating" />
			{/each}
			<input bind:value={feedback} type="text">
			<button type="submit" disabled={feedback ? feedback.length < 10 : true}>Send</button>
		</fieldset>
	</form>
	<div>
		<p>{reviewCount} Reviews</p>
		<p>{average ? 'Ratings Average: ' + average : 'No ratings'}</p>
	</div>
	<div>
		{#each reviews as review}
			<div>
				<span>{review.rating}</span>
				<p>{review.feedback}</p>
				<button on:click={removeReview(review)}>x</button>
			</div>
		{/each}
	</div>
</main>

<style>
</style>