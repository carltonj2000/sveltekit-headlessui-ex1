<script>
	import {
		Listbox,
		ListboxButton,
		ListboxOptions,
		ListboxOption
	} from '@rgossiaux/svelte-headlessui';

	import 'iconify-icon';

	const people = [
		{ id: 1, name: 'Durward Reynolds', unavailable: false },
		{ id: 2, name: 'Kenton Towne', unavailable: false },
		{ id: 3, name: 'Therese Wunsch', unavailable: false },
		{ id: 4, name: 'Benedict Kessler', unavailable: true },
		{ id: 5, name: 'Katelyn Rohan', unavailable: false }
	];

	let selectedPerson = people[0];
</script>

<div class="listbox">
	<Listbox value={selectedPerson} on:change={(e) => (selectedPerson = e.detail)}>
		<ListboxButton class="button">
			{selectedPerson.name} <iconify-icon icon="entypo:select-arrows" />
		</ListboxButton>
		<ListboxOptions class="options">
			{#each people as person (person.id)}
				<ListboxOption
					class="option"
					value={person}
					disabled={person.unavailable}
					let:active
					let:selected
				>
					<span class:active class:selected>{person.name}</span>
				</ListboxOption>
			{/each}
		</ListboxOptions>
	</Listbox>
</div>

<style>
	.listbox {
		max-width: 280px;
		position: relative;
		font-weight: 500;
		color: hsl(220 20% 98%);
	}

	.listbox :global(.button) {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 1rem;
		font-family: inherit;
		font-size: inherit;
		color: inherit;
		background-color: hsl(220 20% 2%);
		border: none;
		border-radius: 10px;
	}

	.listbox :global(.options) {
		position: absolute;
		top: 44px;
		right: 0;
		left: 0;
		padding: 1rem;
		background-color: hsl(220 20% 4%);
		border-radius: 10px;
		list-style: none;
	}

	.listbox :global(.option) {
		padding: 0.8rem 0.4rem;
		cursor: pointer;
	}

	.listbox :global(.option[aria-disabled='true']) {
		color: hsl(220 20% 30%);
	}

	.listbox :global(.active) {
		color: hsl(220 80% 70%);
	}

	.listbox :global(.active)::before {
		content: '👉️ ';
	}

	.listbox :global(.selected) {
		font-weight: 700;
	}

	.listbox :global(.selected)::before {
		content: '⭐️ ';
	}
</style>
