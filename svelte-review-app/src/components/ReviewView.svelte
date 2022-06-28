<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let review;

  function handleClick() {
    dispatch('remove', review)
  }
</script>

<div>
  <span>{review.rating}</span>
  <p>{review.feedback}</p>
  <button on:click={handleClick}>x</button>
</div>

<style>

</style>