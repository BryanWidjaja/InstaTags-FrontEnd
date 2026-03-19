<script lang="ts">
    import type { Snippet } from 'svelte';
    import Siema from 'siema';

    let {
        perPage = 3,
        loop = true,
        autoplay = 0,
        duration = 200,
        easing = 'ease-out',
        startIndex = 0,
        draggable = true,
        multipleDrag = true,
        dots = true,
        controls = true,
        threshold = 20,
        rtl = false,
        children,
        leftControl,
        rightControl,
    }: {
        perPage?: number | Record<string, number>;
        loop?: boolean;
        autoplay?: number;
        duration?: number;
        easing?: string;
        startIndex?: number;
        draggable?: boolean;
        multipleDrag?: boolean;
        dots?: boolean;
        controls?: boolean;
        threshold?: number;
        rtl?: boolean;
        children: Snippet;
        leftControl?: Snippet;
        rightControl?: Snippet;
    } = $props();

    let siema: HTMLDivElement;
    let controller: any = $state(null);
    let timer: ReturnType<typeof setInterval> | undefined;
    let currentIndex = $state(0);

    let pips = $derived(controller ? controller.innerElements : []);
    let currentPerPage = $derived(controller ? controller.perPage : (typeof perPage === 'number' ? perPage : 1));
    let totalDots = $derived(controller ? Math.ceil(controller.innerElements.length / currentPerPage) : 0);

    $effect(() => {
        controller = new Siema({
            selector: siema,
            perPage: typeof perPage === 'object' ? perPage : Number(perPage),
            loop,
            duration,
            easing,
            startIndex,
            draggable,
            multipleDrag,
            threshold,
            rtl,
            onChange: handleChange,
        });

        if (autoplay) {
            timer = setInterval(right, autoplay);
        }

        return () => {
            if (autoplay && timer) clearInterval(timer);
            if (controller) controller.destroy();
        };
    });

    function handleChange() {
        if (controller) currentIndex = controller.currentSlide;
    }

    function isDotActive(idx: number, dotIndex: number) {
        let ci = idx;
        if (ci < 0) ci = pips.length + ci;
        return ci >= dotIndex * currentPerPage && ci < dotIndex * currentPerPage + currentPerPage;
    }

    function left() {
        controller?.prev();
    }

    function right() {
        controller?.next();
    }

    function go(index: number) {
        controller?.goTo(index);
    }

    function pause() {
        if (timer) clearInterval(timer);
    }

    function resume() {
        if (autoplay) {
            timer = setInterval(right, autoplay);
        }
    }

    function handleControlClick(action: () => void) {
        action();
        if (autoplay) {
            pause();
            resume();
        }
    }
</script>

<div class="carousel">
    <div class="carousel-viewport">
        <div class="slides" bind:this={siema}>
            {@render children()}
        </div>
        
        <div class="shadow-left"></div>
        <div class="shadow-right"></div>
    </div>

    {#if controls}
        <button class="left" onclick={() => handleControlClick(left)} aria-label="left">
            {#if leftControl}
                {@render leftControl()}
            {/if}
        </button>

        <button class="right" onclick={() => handleControlClick(right)} aria-label="right">
            {#if rightControl}
                {@render rightControl()}
            {/if}
        </button>
    {/if}

    {#if dots}
        <ul>
            {#each Array(totalDots) as _, i}
                <li class={isDotActive(currentIndex, i) ? 'active' : ''}>
                    <button
                        onclick={() => go(i * currentPerPage)}
                        aria-label="Go to slide {i + 1}"
                    ></button>
                </li>
            {/each}
        </ul>
    {/if}
</div>

<style>
    .carousel {
        position: relative;
        width: 100%;
        max-width: 100vw;
    }

    .carousel-viewport {
        position: relative;
        width: 100%;
        overflow: hidden;
    }

    .slides {
    	width: 100%;
		max-width: 600px;
		margin: 0 auto;
		overflow: visible !important;
    }

    .slides :global(> div > div) {
        display: flex !important;
        justify-content: center;
        align-items: center;
        padding: 0 1rem;
        box-sizing: border-box;
    }

    .shadow-left,
    .shadow-right {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 15vw;
        max-width: 250px;
        z-index: 10;
        pointer-events: none;
    }

    .shadow-left {
        left: 0;
        background: linear-gradient(to right, rgb(45, 45, 45, 0.75), #2D2D2D00);
    }

    .shadow-right {
        right: 0;
        background: linear-gradient(to left, rgb(45, 45, 45, 0.75), #2D2D2D00);
    }

    button {
        position: absolute;
        width: 40px;
        height: 40px;
        top: 50%;
        z-index: 50;
        transform: translateY(-50%);
        border: none;
        background-color: transparent;
        cursor: pointer;
        color: var(--gray-200);
		background-color: #1c1c1c80;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 999px;
    }

    button:focus {
        outline: none;
    }

    .left {
        left: 1.5vw;
    }

    .right {
        right: 1.5vw;
    }

    ul {
        list-style-type: none;
        display: flex;
        justify-content: center;
        width: 100%;
        padding: 0;
        margin-top: 1.5rem;
		gap: 1rem;
    }

    ul li {
        border-radius: 100%;
        background-color: var(--gray-500);
        height: 0.75rem;
        width: 0.75rem;
        cursor: pointer;
    }

    ul li button {
        all: unset;
        width: 100%;
        height: 100%;
        display: block;
        cursor: pointer;
    }

    ul li:hover {
        background-color: var(--gray-400);
    }

    ul li.active {
        background-color: var(--gray-300);
    }
</style>