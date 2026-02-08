<script lang="ts">
	import logo from '$lib/assets/msu(1).png';

	let mobileMenuOpen = $state(false);

	function toggleMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}
</script>

<nav class="navbar">
	<div class="nav-container">
		<a href="/" class="nav-logo">
			<img src={logo} alt="MSU Logo" class="logo-img" />
			<span class="logo-text">Game Design Club</span>
		</a>

		<button class="mobile-toggle" onclick={toggleMenu} aria-label="Toggle menu">
			<span class="hamburger" class:open={mobileMenuOpen}></span>
		</button>

		<ul class="nav-links" class:open={mobileMenuOpen}>
			<li><a href="/#about" onclick={() => mobileMenuOpen = false}>About</a></li>
			<li><a href="/#goals" onclick={() => mobileMenuOpen = false}>Goals</a></li>
			<li><a href="/#activities" onclick={() => mobileMenuOpen = false}>Activities</a></li>
			<li><a href="/#events" onclick={() => mobileMenuOpen = false}>Events</a></li>
			<li><a href="/join-us" class="cta-link" onclick={() => mobileMenuOpen = false}>Join Us</a></li>
		</ul>
	</div>
</nav>

<style>
	.navbar {
		background: #2b70e4; /* MSU Blue */
		position: sticky;
		top: 0;
		z-index: 1000;
		border-bottom: 3px solid #ffc72c; /* MSU Yellow */
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
	}

	.nav-container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 1rem 2rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.nav-logo {
		display: flex;
		align-items: center;
		gap: 0.75rem;
		text-decoration: none;
		color: white;
		font-weight: 600;
		font-size: 1.2rem;
		transition: opacity 0.3s;
	}

	.nav-logo:hover {
		opacity: 0.9;
	}

	.logo-img {
		height: 45px;
		width: auto;
	}

	.logo-text {
		color: white;
	}

	.nav-links {
		display: flex;
		list-style: none;
		gap: 2rem;
		align-items: center;
		margin: 0;
		padding: 0;
	}

	.nav-links a {
		color: white;
		text-decoration: none;
		font-weight: 500;
		transition: color 0.3s;
		position: relative;
	}

	.nav-links a::after {
		content: '';
		position: absolute;
		bottom: -5px;
		left: 0;
		width: 0;
		height: 2px;
		background: #ffc72c;
		transition: width 0.3s;
	}

	.nav-links a:hover {
		color: #ffc72c;
	}

	.nav-links a:hover::after {
		width: 100%;
	}

	.cta-link {
		padding: 0.6rem 1.5rem;
		background: #ffc72c;
		border-radius: 5px;
		color: #2b70e4 !important;
		font-weight: 600;
		transition: transform 0.2s, box-shadow 0.2s;
	}

	.cta-link:hover {
		transform: translateY(-2px);
		box-shadow: 0 4px 8px rgba(255, 199, 44, 0.3);
	}

	.cta-link::after {
		display: none;
	}

	/* Mobile menu toggle */
	.mobile-toggle {
		display: none;
		background: none;
		border: none;
		cursor: pointer;
		padding: 0.5rem;
	}

	.hamburger {
		display: block;
		width: 25px;
		height: 2px;
		background: white;
		position: relative;
		transition: background 0.3s;
	}

	.hamburger::before,
	.hamburger::after {
		content: '';
		position: absolute;
		width: 25px;
		height: 2px;
		background: white;
		transition: transform 0.3s;
	}

	.hamburger::before {
		top: -8px;
	}

	.hamburger::after {
		bottom: -8px;
	}

	.hamburger.open {
		background: transparent;
	}

	.hamburger.open::before {
		transform: rotate(45deg) translate(5px, 5px);
	}

	.hamburger.open::after {
		transform: rotate(-45deg) translate(6px, -6px);
	}

	/* Responsive */
	@media (max-width: 768px) {
		.mobile-toggle {
			display: block;
		}

		.nav-links {
			position: absolute;
			top: 100%;
			left: 0;
			right: 0;
			flex-direction: column;
			background: #2b70e4;
			padding: 2rem;
			gap: 1.5rem;
			transform: translateY(-100%);
			opacity: 0;
			visibility: hidden;
			transition: transform 0.3s, opacity 0.3s, visibility 0.3s;
			border-bottom: 3px solid #ffc72c;
		}

		.nav-links.open {
			transform: translateY(0);
			opacity: 1;
			visibility: visible;
		}

		.nav-links a::after {
			display: none;
		}
	}
</style>
