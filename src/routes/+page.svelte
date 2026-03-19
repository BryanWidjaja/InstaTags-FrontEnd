<script lang="ts">
	import SectionHeader from "$lib/components/SectionHeader.svelte";
	import FaqContainer from "$lib/components/FaqContainer.svelte";
</script>

<section class="hero">
	
</section>

<section class="features">
	
</section>

<section class="testimonials">
	
</section>

<section class="faq">
	<SectionHeader text="Frequently Asked Questions" />
	<div class="faq-containers-container">
		<FaqContainer 
			question="Is Instatags really free?"
			answer='
				Yes! We are an open-source project built by a community of creators. There are no subscriptions, no hidden fees, and no "premium" tiers. Just free tools for everyone.
			'
		/>
		<FaqContainer 
			question="How do I generate tags?"
			answer="
				It's easy: either upload an image directly to our web app or use our browser extension to right-click and analyze any image you see while surfing the web.
			"
		/>
		<FaqContainer 
			question="Do I need to create an account?"
			answer="
				Nope. You can start generating hashtags immediately without giving us your email or creating a password. We value your time as much as your creativity.
			"
		/>
		<FaqContainer 
			question="How does the AI choose the hashtags?"
			answer="
				Our AI analyzes the objects, mood, and context of your photo to suggest a mix of trending and niche tags designed to boost your reach and engagement on Instagram.
			"
		/>
		<FaqContainer 
			question="Is my data safe?"
			answer="
				Absolutely. Because we are open-source, our code is transparent. We don't store your images or sell your data. We're here to help you grow, not to track you.
			"
		/>
	</div>
</section>

<style>
	section {
		min-height: 100vh;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	.faq {
		gap: 2rem;
		padding: 5rem 0rem;
		justify-content: flex-start;
	}

	.faq-containers-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		gap: 1.5rem;
	}
</style>
