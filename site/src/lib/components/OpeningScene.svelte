<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper, contentContainer, captionBox;
	let map,
		areaMap,
		subdivisions,
		lots,
		parcels,
		roads,
		platMap,
		vintageMap;
	let title, subhead;
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7, cap8;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=6000',
				pin: true,
				scrub: 2,
				anticipatePin: 1,
			}
		});

		tl.to(areaMap, { opacity: 1, duration: 0 }, 0)
			.to(subdivisions, { opacity: 1, duration: 1 }, '>3')
			.add('subdivisionsIn', '<')
			.to(lots, { opacity: 1, duration: 1 }, '>3')
			.add('lotsIn', '<')
			.to(parcels, { opacity: 1, duration: 1 }, '>3')
			.add('parcelsIn', '<')
			.to(roads, { opacity: 1, duration: 1 }, '>3')
			.to(subdivisions, { opacity: 0, duration: 1 }, '<')
			.to(lots, { opacity: 0, duration: 1 }, '<')
			.to(parcels, { opacity: 0, duration: 1 }, '<')
			.add('roadsIn', '<')
			.to(vintageMap, { opacity: 1, duration: 1 }, '>7')
			.to(areaMap, { opacity: 0, duration: 1 }, '<')
			.to(roads, { opacity: 0, duration: 1 }, '<')
			.add('vintageIn', '<')
			// .add('mapsRise', '>15')
			.to(platMap, { opacity: 1, duration: 3 }, '>20')
			.to(vintageMap, { opacity: 0, duration: 3 }, '<')

		tl.to(cap1, { opacity: 1, duration: 0 }, 0)
			.to(cap1, { opacity: 0, duration: 0.25 }, 'subdivisionsIn')
			.to(cap2, { opacity: 1, duration: 1.5 }, 'subdivisionsIn')
			.to(cap2, { opacity: 0, duration: 0.25 }, 'lotsIn')
			.to(cap3, { opacity: 1, duration: 1.5 }, 'lotsIn')
			.to(cap3, { opacity: 0, duration: 0.25 }, 'parcelsIn')
			.to(cap4, { opacity: 1, duration: 1.5 }, 'parcelsIn')
			.to(cap4, { opacity: 0, duration: 0.1 }, 'roadsIn')
			.to(cap5, { opacity: 1, duration: 1.5 }, 'roadsIn')
			.to(cap5, { opacity: 0, duration: 0.1 }, 'vintageIn')
			.to(cap6, { opacity: 1, duration: 1.5 }, 'vintageIn')
			.to(cap6, { opacity: 0, duration: 0.1 }, '>5')
			.to(cap7, { opacity: 1, duration: 1.5 }, '<')
			.to(cap7, { opacity: 0, duration: 0.1 }, '>5')
			.to(cap8, { opacity: 1, duration: 1.5 }, '<')
			.add('lastCaptionIn', '>')

		tl
			// .to(
			// 		pinnedWrapper,
			// 		{ backgroundColor: '#e7eddd', duration: 2 },
			// 		'vintageIn'
			// 	)
			// .to(background, { scale: 3, xPercent: -20, duration: 1 }, 'platIn')
			.to(map, { y: '-100vh', duration: 10, ease: 'none' }, 'lastCaptionIn+=5')
			.to(captionBox, { y: '-125vh', duration: 10, ease: 'none' }, 'lastCaptionIn+=5')
			.to(pinnedWrapper, { backgroundColor: '#ffffff', duration: 5, ease: 'none' }, 'lastCaptionIn+=5')
			// .fromTo(title, { y: '150vh' }, { y: '-130vh', duration: 5, ease: 'none' }, 'lastCaptionIn+=5');
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="content-container" bind:this={contentContainer}>
		<div class="map" bind:this={map}>
			<img bind:this={areaMap} src={`${base}/images/opening/areamap.png`} alt="" class="layer" />
			<img
				bind:this={subdivisions}
				src={`${base}/images/opening/areamap-subdivisions.png`}
				alt=""
				class="layer"
			/>
			<img bind:this={lots} src={`${base}/images/opening/areamap-lots.png`} alt="" class="layer" />
			<img
				bind:this={parcels}
				src={`${base}/images/opening/areamap-parcels.png`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={roads}
				src={`${base}/images/opening/areamap-roads.png`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={vintageMap}
				src={`${base}/images/opening/vintagemap.png`}
				alt=""
				class="layer"
			/>
			<img bind:this={platMap} src={`${base}/images/opening/platmap.png`} alt="" class="layer" />
		</div>
		<div class="caption-box" bind:this={captionBox}>
			<p class="caption" bind:this={cap1}>
				In the 1960s, a company acquired a stretch of Chihuahuan desert east of El Paso, Texas.
			</p>
			<p class="caption" bind:this={cap2}>It split it into subdivisions...</p>
			<p class="caption" bind:this={cap3}>
				split those into hundreds of lots...
			</p>
			<p class="caption" bind:this={cap4}>
				and those into thousands of parcels.
			</p>
			<p class="caption" bind:this={cap5}>
				An entire network of streets and cul-de-sacs was etched into the desert scrub.
			</p>
			<p class="caption" bind:this={cap6}>
				Door-to-door sales reps, dinner parties, and glossy mailers persuaded buyers<br> who had never set foot in the desert --
			</p>
			<p class="caption" bind:this={cap7}>
				some as far away as Guam and Germany.
			</p>
			<p class="caption" bind:this={cap8}>Over 100,000 parcels were sold.</p>
		 </div>
	</div>
	<!-- <h1 bind:this={title}>Phantom Plats</h1> -->
</div>

<style>
	.wrapper {
		position: relative;
		height: 100vh;
		height: 100lvh;
		width: 100%;
		overflow: hidden;
		background-color: #fcf9f5;
	}

	.content-container {
		position: absolute;
		top: 25%;
		left: 50%;
		transform: translate(-50%);
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		max-width: 100%;
		/* max-height: 70vh; */
		z-index: 0;
		/* border: 1px solid black; */
	}

	.map {
		position: relative;
		width: auto;
		height: min(60vh, 80vw);
		aspect-ratio: 5/4;
		max-width: 100%;
		z-index: 0;
		/* border: 1px solid red; */
	}

	.layer {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: contain;
		opacity: 0;
	}

	.caption-box {
		position: relative;
		width: clamp(200px, 70dvw, 450px);
		height: 7rem;
		z-index: 3;
		/* border: 1px solid blue; */
	}

	.caption {
		position: absolute;
		top: 0;
		left: 0;
		/* top: 75%;
		left: 50%;
        transform: translate(-50%); */
		width: clamp(200px, 70dvw, 450px);
		font-family: 'Epilogue', 'Host Grotesk', serif;
		font-weight: 300;
		line-height: 1.3;
		text-align: center;
		padding: 6px;
		/* background-color: #ffffff; */
		/* border: 1px solid black; */
		border-radius: 8px;
		z-index: 3;
		opacity: 0;
		/* border: 1px solid green; */
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
</style>
