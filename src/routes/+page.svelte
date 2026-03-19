<script lang="ts">
	import SectionHeader from "$lib/components/SectionHeader.svelte";
	import TestimonialCard from "$lib/components/TestimonialCard.svelte";
	import Carousel from "$lib/components/Carousel.svelte";
	import FaqContainer from "$lib/components/FaqContainer.svelte";

	const testimonials = [
		{
			quote: "InstaTags completely changed how I handle my posts. What used to take minutes now takes seconds. It's simple, fast, and incredibly reliable.",
			name: "Elon Musk",
			title: "CEO of Tesla and SpaceX",
		},
		{
			quote: "I was surprised at how intuitive it is. No learning curve, no confusion — just instant results. Highly recommended!",
			name: "Jensen Huang",
			title: "Co-founder and CEO of NVIDIA",
		},
		{
			quote: "This tool is a game-changer. It's fast, smart, and makes hashtagging feel seamless. I can't imagine going back to doing it manually.",
			name: "Mary Barra",
			title: "Chair and CEO of General Motors",
		},
		{
			quote: "As someone who values efficiency, InstaTags delivers exactly that. It saves me time and keeps my content optimized without any hassle.",
			name: "Sundar Pichai",
			title: "CEO of Google and Alphabet Inc.",
		},
		{
			quote: "I love how effortless everything feels. The interface is clean, and generating hashtags is instant. It's become part of my daily workflow.",
			name: "Satya Nadella",
			title: "Chairman and CEO of Microsoft",
		},
	];
</script>

<section class="hero">
	
</section>

<section class="features">
	
</section>

<section class="testimonials">
	<SectionHeader text="Trusted by Industry Leaders" />
	<div class="carousel-container">
		<Carousel perPage={1} loop={true} autoplay={5000} dots={true} controls={true} duration={300}>
			{#each testimonials as testimonial}
				<TestimonialCard
					quote={testimonial.quote}
					name={testimonial.name}
					title={testimonial.title}
				/>
			{/each}

			{#snippet leftControl()}
				<img src="/icons/left-arrow.svg" alt="<">
			{/snippet}

			{#snippet rightControl()}
				<img src="/icons/right-arrow.svg" alt=">">
			{/snippet}
		</Carousel>
	</div>
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
		gap: 2rem;
		padding: 5rem 0rem;
	}

	.features {
		background: linear-gradient(#3A4E7200 83%, #3A4E7226);
	}

	.testimonials {
		background-color: #3A4E7226;
	}

	.faq {
		justify-content: flex-start;
		background: linear-gradient(#3A4E7226, #3A4E7200 17%);
	}

	.faq-containers-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		gap: 1.5rem;
	}

	.carousel-container {
		width: 100%;
		max-width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
