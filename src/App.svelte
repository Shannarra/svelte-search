<script lang="typescript">
	import Users from './Users.svelte';
	import {nameStore, usersStore} from './stores';

	import {onMount} from 'svelte';

	onMount(() => {
		setTimeout(() =>{
			allUsersList = $usersStore;
		}, 50)
	});


	export let name: string;

	let allUsersList = $usersStore;

	const liveUpdate = () => {
		if (name?.trim().length > 0)
		{	
			name = name.trim();
			nameStore.set(name);
			
			let users = $usersStore.filter(x => x.login.toLowerCase().includes(name));
			console.log(users);

			if (users)
				allUsersList = [...users];
			else
				allUsersList = $usersStore;
		}
	}

	
</script>

<main>
	<input type="text" bind:value={name} on:keyup={() => liveUpdate()} placeholder="search!" />

	{#if (name)}
		<h1>Search results for "{name}".</h1>
	{/if}
	<Users {allUsersList}/>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>