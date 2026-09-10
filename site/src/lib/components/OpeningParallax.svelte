<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);

	let pinnedWrapper;
	let background, areaMap, boundary, subdivisions, lots, roads, labels, platMap, vintageMap;
	let title, subhead;
	let cap1, cap2, cap3, cap4, cap5, cap6;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=6000',
				pin: true,
				anticipatePin: 1,
				scrub: 1,
				markers: true
			}
		});

		// tl.to(areaMap, { opacity: 1, duration: 0 }, 0)
		// 	.to(boundary, { opacity: 1, duration: 0 }, 0)
		// 	.to(subdivisions, { opacity: 1, duration: 3 }, '>1')
		// 	.add('subdivisionsIn', '<')
		// 	.to(lots, { opacity: 1, duration: 3 }, '>1')
		// 	.add('lotsIn', '<')
		// 	.to(roads, { opacity: 1, duration: 3 }, '>2')
		// 	.add('roadsIn', '<')
		// 	.to(subdivisions, { opacity: 0, duration: 0.1 }, '<')
		// 	.to(lots, { opacity: 0, duration: 0.1 }, '<')
		// 	.to(vintageMap, { opacity: 1, duration: 0.5 }, '>5')
		// 	.add('vintageIn', '<')
		// 	.to(areaMap, { opacity: 0, duration: 0.1 }, '<')
		// 	.to(roads, { opacity: 0, duration: 0.1 }, '<')
		// 	.to(vintageMap, { opacity: 0, duration: 1 }, '>5')
		// 	.to(platMap, { opacity: 1, duration: 1 }, '>')
		// 	.add('platIn', '<');

		tl.fromTo(background, { yPercent: 30 }, { yPercent: 10, duration: 1 }, 0)
			.fromTo(title, { y: '30dvh' }, { y: '-70dvh', duration: 1 }, 0);


		// tl.to(cap1, { opacity: 1, duration: 0 }, 0)
		// 	.to(cap1, { opacity: 0, duration: 0.1 }, 'subdivisionsIn')
		// 	.to(cap2, { opacity: 1, duration: 0.25 }, 'subdivisionsIn')
		// 	.to(cap2, { opacity: 0, duration: 0.1 }, 'lotsIn')
		// 	.to(cap3, { opacity: 1, duration: 0.25 }, 'lotsIn')
		// 	.to(cap3, { opacity: 0, duration: 0.1 }, 'roadsIn')
		// 	.to(cap4, { opacity: 1, duration: 0.25 }, 'roadsIn')
		// 	.to(cap4, { opacity: 0, duration: 0.1 }, 'vintageIn')
		// 	.to(cap5, { opacity: 1, duration: 0.25 }, 'vintageIn');

		// tl.fromTo(cap1, { y: '100svh' }, { y: '-30svh', duration: 3 }, 0)
		// 	.fromTo(cap2, { y: '100svh' }, { y: '-30svh', duration: 3 }, 'subdivisionsIn')
		// 	.fromTo(cap3, { y: '100svh' }, { y: '-30svh', duration: 3 }, 'lotsIn')
		// 	.fromTo(cap4, { y: '100svh' }, { y: '-30svh', duration: 3 }, 'roadsIn')
		// 	.fromTo(cap5, { y: '100svh' }, { y: '-30svh', duration: 3 }, 'vintageIn')
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="bg-image" bind:this={background} data-speed="0.1">
		<img bind:this={platMap} src={`${base}/images/opening/test-opening2.png`} alt="" class="map" />
	</div>
	<h1 bind:this={title} data-speed="0.6">Phantom Plats</h1>
</div>


<style>
	.wrapper {
		position: relative;
		height: 100dvh;
		width: 100%;
		overflow: hidden;
		/* background-color: #e7eddd; */
		/* background-color: #fcf9f5; */
	}

	.background {
		position: absolute;
		inset: 0;
	}

	/* .map {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		width: 100%;
	} */

	.bg-image {
		position: absolute;
		top: 10%;
		right: 10%;
		width: 300%;
		height: 300%;
		object-fit: cover;
	}

	h1 {
		font-family: 'Josefin Sans';
		font-style: italic;
		font-weight: 600;
		font-size: clamp(2rem, 20vw, 8rem);
		color: white;
		-webkit-text-stroke: 1px black;
		position: absolute;
		bottom: 0;
		left: 50%;
		transform: translate(-50%);
		z-index: 1;
	}

	h2 {
		font-family: 'Josefin Sans';
		font-style: italic;
		font-weight: 300;
		/* font-size: clamp(2rem, 20vw, 3rem); */
		font-size: 1.5rem;
		color: black;
		/* -webkit-text-stroke: 1px black; */
		position: absolute;
		top: 30%;
		left: 50%;
		transform: translate(-50%);
		z-index: 1;
		/* white-space: nowrap; */
	}

	.caption-box {
		position: absolute;
		top: 15%;
		left: 20%;
		/* transform: translate(-50%); */
		width: clamp(200px, 35dvw, 450px);
		padding: 6px;
		z-index: 3;
		background-color: #ffffff;
		border: 1px solid black;
		border-radius: 8px;
		line-height: 1.3;
		font-family: 'Epilogue', 'Host Grotesk', serif;
		font-weight: 300;
		/* font-size: 1.2rem; */
		opacity: 0;
	}

	.caption {
		/* position: absolute; */
		inset: 0;
		opacity: 0;
	}
</style>
