<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let background, areaMap, boundaryDashed, boundary, subdivisions, lots, parcels, roads, platMap, vintageMap;
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
				ease: 'none'
				// markers: true
			}
		});

		tl.to(areaMap, { opacity: 1, duration: 0 }, 0)
			.to(boundaryDashed, { opacity: 1, duration: 0 }, 0)
			.to(subdivisions, { opacity: 1, duration: 1.5 }, '>1')
			.add('subdivisionsIn', '<')
			.to(lots, { opacity: 1, duration: 1.5 }, '>1')
			.add('lotsIn', '<')
			.to(parcels, { opacity: 1, duration: 1.5 }, '>1')
			.add('parcelsIn', '<')
			.to(roads, { opacity: 1, duration: 1.5 }, '>2')
			.to(boundary, { opacity: 1, duration: 1.5 }, '<')
			.to(boundaryDashed, { opacity: 0, duration: 0 }, '<')
			.add('roadsIn', '<')
			.to(subdivisions, { opacity: 0, duration: 1.5 }, '<')
			.to(lots, { opacity: 0, duration: 1.5 }, '<')
			.to(parcels, { opacity: 0, duration: 1.5 }, '<')
			.to(vintageMap, { opacity: 1, duration: 1.5 }, '>5')
			.add('vintageIn', '<')
			.to(areaMap, { opacity: 0, duration: 0.5 }, '<')
			.to(boundary, { opacity: 0, duration: 0.5 }, '<')
			.to(roads, { opacity: 0, duration: 0.5 }, '<')
			.to(vintageMap, { opacity: 0, duration: 3 }, '>5')
			.to(platMap, { opacity: 1, duration: 3 }, '<')
			.add('platIn', '<');

		tl.to(cap1, { opacity: 1, duration: 0 }, 0)
			.to(cap1, { opacity: 0, duration: 0.25 }, 'subdivisionsIn')
			.to(cap2, { opacity: 1, duration: 1.5 }, 'subdivisionsIn')
			.to(cap2, { opacity: 0, duration: 0.25 }, 'lotsIn')
			.to(cap3, { opacity: 1, duration: 1.5 }, 'lotsIn')
			.to(cap3, { opacity: 0, duration: 0.1 }, 'roadsIn')
			.to(cap4, { opacity: 1, duration: 1.5 }, 'roadsIn')
			.to(cap4, { opacity: 0, duration: 0.1 }, 'vintageIn')
			.to(cap5, { opacity: 1, duration: 1.5 }, 'vintageIn')
			.to(cap5, { opacity: 0, duration: 0.1 }, '>3')
			.to(cap6, { opacity: 1, duration: 1.5 }, '<')
			.to(cap6, { opacity: 0, duration: 1.5 }, 'platIn');

		tl
			.to(
					pinnedWrapper,
					{ backgroundColor: '#e7eddd', duration: 2 },
					'vintageIn'
				)
			// .to(background, { scale: 3, xPercent: -20, duration: 1 }, 'platIn')
			.fromTo(background, { y: '10dvh'}, { y: '-30dvh', duration: 5 }, 'platIn')
			.to(pinnedWrapper, { backgroundColor: '#ffffff', duration: 5 }, 'platIn')
			.fromTo(title, { y: '50dvh' }, { y: '-130dvh', ease: 'none', duration: 5 }, 'platIn');
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="background" bind:this={background} data-speed="0.1">
		<img bind:this={areaMap} src={`${base}/images/opening/areamap.png`} alt="" class="map" />
		<img
			bind:this={boundaryDashed}
			src={`${base}/images/opening/areamap-boundary-dashed.png`}
			alt=""
			class="map"
		/>
		<img
			bind:this={boundary}
			src={`${base}/images/opening/areamap-boundary.png`}
			alt=""
			class="map"
		/>
		<img bind:this={subdivisions} src={`${base}/images/opening/areamap-subdivisions.png`} alt="" class="map" />
		<img bind:this={lots} src={`${base}/images/opening/areamap-lots.png`} alt="" class="map" />
		<img bind:this={parcels} src={`${base}/images/opening/areamap-parcels.png`} alt="" class="map" />
		<img bind:this={roads} src={`${base}/images/opening/areamap-roads.png`} alt="" class="map" />
		<img bind:this={vintageMap} src={`${base}/images/opening/vintagemap2.png`} alt="" class="map" />
		<img
			bind:this={platMap}
			src={`${base}/images/opening/platmap.png`}
			alt=""
			class="map"
		/>
	</div>
	<h1 bind:this={title} data-speed="0.6">Phantom Plats</h1>
	<p class="caption-box" bind:this={cap1}>
		In the 1960s, a real estate development company called the Horizon Corporation acquired a patch of desert between El Paso, Texas and the Hueco Mountains.
	</p>
	<p class="caption-box" bind:this={cap2}>
		It split this desert into subdivisions
	</p>
	<p class="caption-box" bind:this={cap3}>
		... split those into hundreds of lots, and those further into thousands of parcels.
	</p>
	<p class="caption-box" bind:this={cap4}>
		To give every parcel a real address, an entire network of suburban streets and cul-de-sacs was named and etched into the desert scrub.
	</p>
	<p class="caption-box" bind:this={cap5}>
		Door-to-door salesmen and mail-order brochures convinced prospective buyers as far away as Guam and Germany to invest in a slice of the Southwest.
	</p>
	<p class="caption-box" bind:this={cap6}>
		Over 100,000 parcels were sold.
	</p>
</div>


<style>
	.wrapper {
		position: relative;
		height: 100vh;
		height: 100lvh;
		width: 100%;
		overflow: hidden;
		/* background-color: #e7eddd; */
		background-color: #fcf9f5;
	}

	.background {
		position: absolute;
		inset: 0;
	}

	.map {
		position: absolute;
		top: 25%;
		/* transform: translateY(-50%); */
		width: 100%;
		opacity: 0;
	}

	.bg-image {
		position: absolute;
		bottom: -50%;
		right: 0;
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
		left: 50%;
		transform: translate(-50%);
		width: clamp(200px, 70dvw, 450px);
		padding: 6px;
		z-index: 3;
		background-color: #ffffff;
		border: 1px solid black;
		border-radius: 8px;
		line-height: 1.3;
		font-family: 'Host Grotesk', 'Epilogue', serif;
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
