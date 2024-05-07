<script>
	import { supabase } from '$lib/supabase';

	let promise = supabase.from('countries').select();
	let names = supabase.from('rabbits').select();
	let name = '';
	async function sendName() {
		const response = await fetch('/api/sendName', {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({ name })
		});
		const data = await response.text();
		console.log(data);

		name = '';
		names = supabase.from('rabbits').select();
	}
</script>

<div class="prose">
	<h1>APIs</h1>
	<ul>
		<li><a href="/api/hello?name=Paul">Link zur API mit Query-Parameter</a></li>
		<li><a href="/api/hello/Paul">Link zur API mit Route-Paramter</a></li>
	</ul>

	<form>
		<h2>All my rabbits</h2>
		<input type="text" bind:value={name} /><br /><button class="btn" on:click={sendName}
			>Add rabbit!</button
		>
	</form>

	<h2>Rabbit names</h2>
	{#await names}
		<span class="loadung loading-bars loading-lg text-primary" />
	{:then result}
		<ul>
			{#each result.data as rabbit (rabbit.id)}
				<li>{rabbit.name}</li>
			{/each}
		</ul>
	{/await}
</div>

<!-- <div class="prose">
	<ul>
		<li>
			anstatt eines JS_Objekts das auf der Seite dargestellt wir möchte ich eine Liste aller Länder
		</li>
		<li><span class="loading loading-dots loading-lg" /></li>

		<li>gib die Vercell-Url zu deinem Projekt in Teams ab.</li>
	</ul>
</div>
{#await promise}
	<div><span class="loading loading-dots loading-lg" /></div>
{:then result}
	<ul>
		{#each result.data as country}
			<li>{country.name}</li>
		{/each}
	</ul>
{/await} -->

<!-- {#await promise}
	<div><span class="loading loading-dots loading-lg" /></div>
{:then result}
	<div>{JSON.stringify(result)}</div>
{/await} -->
