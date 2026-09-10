<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);

	let bridge;
    let text;

	onMount(() => {
		const tween = gsap.fromTo(
			bridge,
			{ backgroundColor: '#373b8f' },
			{
				backgroundColor: '#ffffff',
				ease: 'none',
				scrollTrigger: {
					trigger: bridge,
					start: 'top bottom',
					end: 'bottom top',
					scrub: 3
				}
			}
		);

        const tl = gsap.timeline()

        tl.to(text, { opacity: 1, y:0, ease: 'none' }, 0);

        return () => tween.scrollTrigger.kill();
	});
</script>

<div class="bridge" bind:this={bridge}>
    <p bind:this={text} class="bridge-text">Sold a slot of paradise</p>
</div>

<style>
    .bridge {
        height: 60vh;
        width: 100%
    }
</style>