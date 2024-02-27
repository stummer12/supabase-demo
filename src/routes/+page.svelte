<script>
	import { supabase } from '$lib/supabase';

	let promise = supabase.from('countries').select();
</script>

<div class="prose">
	<ul>
		<li>
			anstatt eines JS_Objekts das auf der Seite dargestellt wir möchte ich eine Liste aller Länder
		</li>
		<li>integriere einen Loading Spinner öÄ von daisyUi in dein Projekt</li>

		<li>gib die Vercell-Url zu deinem Projekt in Teams ab.</li>
	</ul>
</div>

{#await promise}
	<div>...loading</div>
{:then result}
	<div>{JSON.stringify(result)}</div>
{/await}
