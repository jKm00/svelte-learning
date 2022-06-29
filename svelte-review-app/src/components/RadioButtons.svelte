<script lang="ts">
  import type { Option } from '../types/Option'
	import { createEventDispatcher } from 'svelte'

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

	const dispatch = createEventDispatcher()

	// Radio buttons state
  let selected: number

	/**
	 * Updates the selected radio button
	 * @param event, the event that is triggered
	 * when a radion button is pressed
	 */
	const onChange = (event: Event): void => {
		selected = event.currentTarget.value
		dispatch('change', selected)
	}
</script>

<div class="radio-wrapper">
  {#each options as option}
    <input 
			id={option.id} 
			type="radio" 
			value={option.value} 
			name="rating" 
			on:change={onChange} 
			checked={selected === option.value} 
		>
    <label for={option.id}>{option.label}</label>
  {/each}
</div>

<style>
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
</style>