<script lang="ts">
  import RadioButtons from "./RadioButtons.svelte";
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  // Form state
  let text = ''
  let rating: number
  let btnDisabled = true
  let min = 10
  let message: string

  /**
   * Enables/disables button base on character inputted
   */
  const handleInput = (): void => {
    if (text.trim().length <= min) {
      message = `Text must be at least ${min} characters`
      btnDisabled = true
    } else {
      message = null
      btnDisabled = false
    }
  }

  /**
   * Dispatches the values in the form to the main app
   * component
   */
  const handleSubmit = (): void => {
    if (rating === undefined) return
    dispatch('submit', {text, rating})
    text = ''
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="box">
  <fieldset>
    <legend>How would you rate your service with us?</legend>
  </fieldset>
  <RadioButtons on:change={(e) => rating = parseInt(e.detail)} />
  <div class="feedback-wrapper">
    <input on:input={handleInput} bind:value={text} type="text" placeholder="Tell us somethinf that keeps you comming back" name="feedback" />
    <button class="submit" type="submit" disabled={btnDisabled}>Send</button>
  </div>
  {#if message}
    <p class="error-indicator">{message}</p>
  {/if}
</form>

<style>
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

  .error-indicator {
    text-align: center;
    font-size: 0.8rem;
  }
</style>