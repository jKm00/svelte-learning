<script lang="ts">
  import type { Review } from "../types/Review";
  import ReviewItem from "./ReviewItem.svelte";

  export let reviews: Review[]
</script>

<div class="review-list">
  {#each reviews as review (review.id)}
    <ReviewItem on:remove {review} />
  {/each}
</div>

<style>
  .review-list {
    display: flex;
		flex-direction: column;
		gap: 1.5rem;
  }
</style>