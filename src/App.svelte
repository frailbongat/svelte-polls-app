<script>
	import Modal from './Modal.svelte'
	import AddPersonForm from './AddPersonForm.svelte'

	let showModal = false

	const toggleModal = () => {
		showModal = !showModal
	}

	let people = [
		{ name: 'yoshi', beltColour: 'black', age: 25, id: 1},
		{ name: 'mario', beltColour: 'orange', age: 45, id: 2},
		{ name: 'luigi', beltColour: 'brown', age: 35, id: 3},
	]

	const handleClick = (id) => {
		people = people.filter(person => person.id !== id)
	}

	const addPerson = (e) => {
		console.log(e.detail)
		people = [e.detail, ...people]
		showModal = false
	}
</script>

<Modal {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>

<main>
	<button on:click={toggleModal}>Open Modal</button>

	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			<p>{person.age} years old, {person.beltColour} belt.</p>
			{#if person.beltColour === 'black'}
				<p><strong>MASTER NINJA</strong></p>
			{/if}
			<button on:click={() => handleClick(person.id)}>delete</button>
		</div>
	{:else}
		<p>There are no people to show...</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>