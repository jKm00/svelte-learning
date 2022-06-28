<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  // Props
  export let review;

  /**
   * Dispatches a remove event containing the review
   */
  function handleClick() {
    dispatch('remove', review)
  }
</script>

<!-- Review -->
<div class="box review">
  <span>{review.rating}</span>
  <p>{review.feedback}</p>
  <button on:click={handleClick}>x</button>
</div>

<style>
  .review {
    position: relative;
    padding: 1rem 2rem;
  }

  .review span {
    --size: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: calc(var(--size) / 2.5 * -1);
    left: calc(var(--size) / 2.5 * -1);
    background-color: #FF69B4;
    color: #fff;
    height: var(--size);
    width: var(--size);
    border-radius: 100vh;
  }

  .review button {
    position: absolute;
    top: 1rem;
    right: 1rem;
    font-weight: bold;
    font-size: 1rem;
  }
</style>