<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { GSDevTools } from "gsap/GSDevTools";
	gsap.registerPlugin(ScrollTrigger, GSDevTools);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper, captionBox;
	let map,
		areaMap,
		subdivisions,
		lots,
		parcels,
		roads,
		platMap,
		vintageMap;
	let title, subhead;
	let cap0, cap1, cap2, cap3, cap4, cap5, cap6, cap7, cap8;

	onMount(() => {
		
		const DEBUG = false;

		const tl = gsap.timeline(
			DEBUG ? {paused: true} : {
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: () => '+=' + Math.min(Math.max(window.innerHeight * 8, 5200), 8800),
				pin: true,
				scrub: 1.5,
				anticipatePin: 1,
				invalidateOnRefresh: true
			}
		});

		tl.to(cap0, { opacity: 1, duration: 0 }, 0)
			.to(cap0, { opacity: 0, duration: 3 }, 3)
			.add('areamapIn', 7)
			.to(areaMap, { opacity: 1, duration: 3 }, 'areamapIn')
			.to(cap1, { opacity: 1, duration: 3 }, 'areamapIn')
			.add('subdivisionsIn', 'areamapIn+=7')
			.to(subdivisions, { opacity: 1, duration: 2 }, 'subdivisionsIn')
			.to(cap1, { opacity: 0, duration: 2 }, 'subdivisionsIn')
			.to(cap2, { opacity: 1, duration: 3 }, 'subdivisionsIn')
			.add('lotsIn', 'subdivisionsIn+=7')
			.to(lots, { opacity: 1, duration: 2 }, 'lotsIn')
			.to(cap2, { opacity: 0, duration: 2 }, 'lotsIn')
			.to(cap3, { opacity: 1, duration: 3 }, 'lotsIn')
			.add('parcelsIn', 'lotsIn+=7')
			.to(parcels, { opacity: 1, duration: 2 }, 'parcelsIn')
			.to(cap3, { opacity: 0, duration: 2 }, 'parcelsIn')
			.to(cap4, { opacity: 1, duration: 3 }, 'parcelsIn')
			.add('roadsIn', 'parcelsIn+=9')
			.to(roads, { opacity: 1, duration: 2 }, 'roadsIn')
			.to(subdivisions, { opacity: 0, duration: 2 }, 'roadsIn')
			.to(lots, { opacity: 0, duration: 2 }, 'roadsIn')
			.to(parcels, { opacity: 0, duration: 2 }, 'roadsIn')
			.to(cap4, { opacity: 0, duration: 2 }, 'roadsIn')
			.to(cap5, { opacity: 1, duration: 3 }, 'roadsIn')
			.add('preVintageFade', 'roadsIn+=9')
			.to(areaMap, { opacity: 0, duration: 3 }, 'preVintageFade')
			.to(roads, { opacity: 0, duration: 3 }, 'preVintageFade')
			.to(cap5, { opacity: 0, duration: 3 }, 'preVintageFade')
			.add('vintageIn', 'preVintageFade+=3')
			.to(vintageMap, { opacity: 1, duration: 6 }, 'vintageIn')
			.to(cap6, { opacity: 1, duration: 6 }, 'vintageIn')
			.add('vintageBeat2', 'vintageIn+=11')
			.to(cap6, { opacity: 0, duration: 2 }, 'vintageBeat2')
			.to(cap7, { opacity: 1, duration: 3 }, 'vintageBeat2')
			.add('contentRises', 'vintageBeat2+=8')
			.to(map, { y: '-100vh', duration: 15, ease: 'none' }, 'contentRises')
			.to(captionBox, { y: '-150vh', duration: 15, ease: 'none' }, 'contentRises')
			.to(pinnedWrapper, { backgroundColor: '#ffffff', duration: 5, ease: 'none' }, 'contentRises')
			.add('platIn', 'contentRises')
			.to(platMap, { opacity: 1, duration: 3 }, 'platIn')
			.to(vintageMap, { opacity: 0, duration: 3 }, 'platIn')

		// tl.to(cap0, { opacity: 1, duration: 0 }, 0)
		// 	.to(cap0, { opacity: 0, duration: 3 }, 3)
		// 	.to(cap1, { opacity: 1, duration: 3 }, 'areamapIn')
		// 	.to(cap1, { opacity: 0, duration: 1 }, 'subdivisionsIn')
		// 	.to(cap2, { opacity: 1, duration: 3 }, 'subdivisionsIn')
		// 	.to(cap2, { opacity: 0, duration: 1 }, 'lotsIn')
		// 	.to(cap3, { opacity: 1, duration: 3 }, 'lotsIn')
		// 	.to(cap3, { opacity: 0, duration: 1 }, 'parcelsIn')
		// 	.to(cap4, { opacity: 1, duration: 3 }, 'parcelsIn')
		// 	.to(cap4, { opacity: 0, duration: 1 }, 'roadsIn')
		// 	.to(cap5, { opacity: 1, duration: 3 }, 'roadsIn')
		// 	.to(cap5, { opacity: 0, duration: 3 }, 'preVintageFade')
		// 	.to(cap6, { opacity: 1, duration: 6 }, 'vintageIn')
		// 	.add('vintageBeat2', '>5')
		// 	.to(cap6, { opacity: 0, duration: 1 }, 'vintageBeat2')
		// 	.to(cap7, { opacity: 1, duration: 3 }, 'vintageBeat2')
		// 	.add('vintageBeat3', '>5')
		// 	.to(cap7, { opacity: 0, duration: 1 }, 'vintageBeat3')
		// 	.to(cap8, { opacity: 1, duration: 3 }, 'vintageBeat3')
		// 	// .add('lastCaptionIn', '>')
		// 	.add('contentRises', '>5')

		// tl.to(map, { y: '-100vh', duration: 10, ease: 'none' }, 'contentRises')
		// 	.to(captionBox, { y: '-150vh', duration: 10, ease: 'none' }, 'contentRises')
		// 	.to(pinnedWrapper, { backgroundColor: '#ffffff', duration: 5, ease: 'none' }, 'contentRises')
			// .fromTo(title, { y: '150vh' }, { y: '-130vh', duration: 5, ease: 'none' }, 'lastCaptionIn+=5');

		if (DEBUG) GSDevTools.create({animation: tl});
		// console.log(tl.labels, tl.duration());
		const sorted = Object.entries(tl.labels).sort((a, b) => a[1] - b[1]);
		console.table(
		sorted.map(([name, time], i) => ({
			name,
			time,
			// gap: i ? +(time - sorted[i + 1][1]).toFixed(1) : 0,
			hold: i < sorted.length - 1
			? +(sorted[i + 1][1] - time).toFixed(1)
			: +(tl.duration() - time).toFixed(1),
			percent: +((time / tl.duration()) * 100).toFixed(1)
		}))
		);
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="intro">
		<p bind:this={cap0}>This is a story about land ownership in the American Southwest.</p>
	</div>
	<div class="content-container">
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
				In the 1960s, a company called the Horizon Corporation acquired a stretch of Chihuahuan desert east of El Paso, Texas.
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
				Door-to-door sales reps, dinner parties, and glossy mailers persuaded buyers who had never set foot in the desert — some as far away as Guam and Germany.
			</p>
			<p class="caption" bind:this={cap7}>Over 100,000 parcels were sold.</p>
		 </div>
	</div>
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
		/* left: 50%;
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

	.intro {
		position: absolute;
		top: 10%;
		left: 50%;
		transform: translate(-50%);
		width: clamp(200px, 70dvw, 450px);
		font-family: 'Josefin Sans';
		font-style: italic;
		font-weight: 300;
		font-size: 1.5rem;
		text-align: center;
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

</style>
