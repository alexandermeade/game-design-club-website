<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import Navbar from '$lib/components/Navbar.svelte';
	
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<Navbar />
{@render children()}

<footer class="footer">
	<div class="footer-content">
		<p>&copy; 2025 MSU Game Design Club. All rights reserved.</p>
		<p>Morehead State University</p>
	</div>
</footer>

<style>
	.footer {
		background: #2b70e4;
		color: white;
		padding: 2rem;
		text-align: center;
		border-top: 3px solid #ffc72c;
	}

	.footer-content {
		max-width: 1200px;
		margin: 0 auto;
	}

	.footer-content p {
		margin: 0.5rem 0;
	}
</style>
