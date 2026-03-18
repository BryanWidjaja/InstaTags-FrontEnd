<script lang="ts">
	import { page } from '$app/state';

	let mobileMenuOpen = $state(false);

	const navLinks = [
		{ href: '/upload', label: 'Upload' },
		{ href: '/how-to-use', label: 'How To Use' },
		{ href: '/about-us', label: 'About Us' }
	];

	const toggleMobileMenu = () => {
		mobileMenuOpen = !mobileMenuOpen;
	}
</script>

<nav class="navbar">
	<a href="/" class="logo">InstaTags</a>

	<button class="mobile-toggle" onclick={toggleMobileMenu} aria-label="Toggle menu">
		<span class="bar" class:open={mobileMenuOpen}></span>
		<span class="bar" class:open={mobileMenuOpen}></span>
		<span class="bar" class:open={mobileMenuOpen}></span>
	</button>

	<div class="nav-links" class:show={mobileMenuOpen}>
		{#each navLinks as link}
			<a
				href={link.href}
				class="nav-link"
				class:active={page.url.pathname === link.href}
				onclick={() => (mobileMenuOpen = false)}
			>
				{link.label}
			</a>
		{/each}
	</div>
</nav>

<style>
	.navbar {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 100;
		padding: 1.5rem 3.5rem;
		backdrop-filter: blur(12px);
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.logo {
		font-family: LaurentianStd-It;
		font-size: 2rem;
		transition: all 0.3s ease;
	}

	.logo:hover {
		opacity: 0.85;
	}

	.nav-links {
		display: flex;
		list-style: none;
		gap: 2rem;
		align-items: center;
	}

	.nav-link {
		font-size: 1.1rem;
		font-weight: 400;
		color: var(--gray-300);
		transition: all 0.3s ease;
		position: relative;
	}

	.nav-link:hover,
	.nav-link.active {
		color: var(--gray-100);
	}

	.nav-link::after {
		content: '';
		position: absolute;
		bottom: -4px;
		left: 0;
		width: 0;
		height: 2px;
		background: var(--primary-500);
		transition: all 0.3s ease;
	}

	.nav-link:hover::after,
	.nav-link.active::after {
		width: 100%;
	}

	.mobile-toggle {
		display: none;
		flex-direction: column;
		gap: 5px;
		background: none;
		border: none;
		padding: 4px;
	}

	.bar {
		display: block;
		width: 24px;
		height: 2px;
		background: var(--gray-100);
		transition: all 0.3s ease;
		border-radius: 1px;
	}

	.bar.open:nth-child(1) {
		transform: rotate(45deg) translate(5px, 5px);
	}

	.bar.open:nth-child(2) {
		opacity: 0;
	}

	.bar.open:nth-child(3) {
		transform: rotate(-45deg) translate(5px, -5px);
	}

	@media (max-width: 768px) {
		.mobile-toggle {
			display: flex;
		}

		.nav-links {
			position: fixed;
			top: 0;
			right: -100%;
			height: 100vh;
			width: 260px;
			flex-direction: column;
			background: var(--color-navy-900);
			padding: 5rem 2rem;
			gap: 1.5rem;
			transition: all 0.3s ease;
			border-left: 1px solid var(--color-navy-600);
		}
		
		.nav-links.show {
			right: 0;
		}
	}
</style>
