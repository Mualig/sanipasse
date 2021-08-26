<script lang="ts">
	import invitedTo from './_invitedToStore';
	import { Row } from 'sveltestrap';
	import Wallet from './wallet.svelte';
	import ShowPromiseError from './_showPromiseError.svelte';
	let links = [
		{ href: '/import/video', text: '📸 Scanner un certificat' },
		{ href: '/import/file', text: '📁 Importer un fichier' },
		{ href: '/import/text', text: '🔗 Entrer un lien TousAntiCovid' }
	];
</script>

<svelte:head>
	<title>SaniBAMHE: Vérification de pass sanitaire</title>
	<meta
		name="description"
		content="SaniBAMHE permet de vérifier les certificats de test et de vaccination,
et d'organiser des évènements en toute sécurité."
	/>
</svelte:head>

<header>
	<h1>Bienvenue sur SaniBAMHE</h1>

	<ShowPromiseError promise={$invitedTo.promise} />

	<p>
		SaniBAMHE est un logiciel libre de vérification des certificats de test ou de vaccination, et
		d'organisation d’événements respectueux des règles sanitaires.
	</p>
	<p>
		La vérification proposée ci-dessous est <a href="apropos#donnees">strictement privée</a>, et
		vos données ne quittent jamais votre appareil.
	</p>
</header>

{#each links as { href, text }, i (href)}
	<Row>
		<a {href} class="btn" class:btn-primary={i == 0}>{text}</a>
	</Row>
{/each}

<footer class="mb-2">
	{#if !$invitedTo.eventId}
		<p>
			<b>SaniBAMHE borne</b> permet de mettre en place une borne autonome de contrôle des passes sanitaires,
			munie d'un scanner de QR code physique ou d’une webcam.
		</p>
		<Row>
			<a href="/borne/config" class="btn btn-primary">🤖 Configurer SaniBAMHE borne</a>
		</Row>
	{/if}
	<Wallet />
</footer>

<style>
	a,
	header,
	footer {
		max-width: 512px;
		margin: 1em auto;
	}
</style>
