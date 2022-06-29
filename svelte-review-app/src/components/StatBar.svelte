<script lang="ts">
  export let reviewCount: number
  export let average: number
</script>

<div class="stats">
  <p>{reviewCount} {reviewCount === 1 ? 'Review' : 'Reviews'}</p>
  <p>{average ? 'Ratings Average: ' + average : 'No ratings'}</p>
</div>

<style>
  .stats {
		display: flex;
		justify-content: space-between;
		color: #fff;
		font-weight: bold;
		margin: 1rem 0;
	}
</style>