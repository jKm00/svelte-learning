<script lang="ts">
	import type { Review } from './types/Review'
	import FeedbackForm from './components/FeedbackForm.svelte';
	import ReviewList from './components/ReviewList.svelte';
	import StatBar from './components/StatBar.svelte';

	// States
	let reviewId = 0
	let reviews: Review[] = []

	// Computed values
	$: reviewCount = reviews.length
	$: average = Math.round(reviews.reduce((subtotal, review) => subtotal + review.rating, 0) / reviews.length * 100) / 100

	/**
	 * Adds a review to the list if all fields are filled
	 */
	const addReview = (e: CustomEvent): void => {
		reviews = [{ id: reviewId++, rating: e.detail.rating, feedback: e.detail.text }, ...reviews]
	}

	/**
	 * Removes a review from the list
	 * @param {CustomEvent} event, the event that is triggered when the remove button
	 * is pressed. Contains the review that is to be deleted
	 */
	function removeReview(event: CustomEvent): void {
		reviews = reviews.filter(r => r !== event.detail)
	}
</script>

<main>
	<FeedbackForm on:submit={addReview} />
	<StatBar {reviewCount} {average} />
	<ReviewList on:remove={removeReview} {reviews} />
</main>

<style>
	main {
		max-width: 50rem;
		margin: auto;
		padding: 2rem 0;
	}
</style>