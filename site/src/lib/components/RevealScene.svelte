<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let map, soldParcels, text, units, water, buildings, unbuiltParcels, roads, roadsWhite, satellite, title, codeLink;
	let keyWrapper, soldKey, waterKey, buildingsKey, unbuiltKey;
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: () => '+=' + Math.min(Math.max(window.innerHeight * 8, 5200), 8800),
				pin: true,
				scrub: 1.5,
				anticipatePin: 1,
				// markers: true,
			}
		});

		tl.add('platMapIn', 0)
			.to(text, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(units, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(roads, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(cap1, { opacity: 1, duration: 3 }, 'platMapIn')
			.add('soldIn', 'platMapIn+=11')
			.to(soldParcels, { opacity: 1, duration: 3 }, 'soldIn')
			.to(cap1, { opacity: 0, duration: 2 }, 'soldIn')
			.to(cap2, { opacity: 1, duration: 3 }, 'soldIn')
			.add('waterIn', 'soldIn+=11')
			.to(water, { opacity: 1, duration: 2 }, 'waterIn')
			.to(buildings, { opacity: 1, duration: 2 }, 'waterIn')
			.to(soldParcels, { opacity: 0.1, duration: 2 }, 'waterIn')
			.to(cap2, { opacity: 0, duration: 2 }, 'waterIn')
			.to(cap3, { opacity: 1, duration: 3 }, 'waterIn')
			.add('unbuiltIn', 'waterIn+=20')
			.to(unbuiltParcels, { opacity: 1, duration: 6 }, 'unbuiltIn')
			.to(soldParcels, { opacity: 0, duration: 2 }, 'unbuiltIn')
			.to(water, { opacity: 0, duration: 2 }, 'unbuiltIn')
			.to(cap3, { opacity: 0, duration: 2 }, 'unbuiltIn')
			.to(cap4, { opacity: 1, duration: 6 }, 'unbuiltIn')
			.add('satellitePartIn', 'unbuiltIn+=20')
			.to(satellite, { opacity: 0.3, duration: 10 }, 'satellitePartIn')
			.to(unbuiltParcels, { opacity: 0.3, duration: 10 }, 'satellitePartIn')
			.to(units, { opacity: 0, duration: 2 }, 'satellitePartIn')
			.to(text, { opacity: 0, duration: 2 }, 'satellitePartIn')
			.to(roads, { opacity: 0, duration: 6 }, 'satellitePartIn+=2')
			.to(roadsWhite, { opacity: 1, duration: 6 }, 'satellitePartIn+=2')
			.add('satelliteFullIn', 'satellitePartIn+=20')
			.to(satellite, { opacity: 1, duration: 6 }, 'satelliteFullIn')
			.to(unbuiltParcels, { opacity: 0, duration: 6 }, 'satelliteFullIn')
			.to(cap4, { opacity: 0, duration: 2 }, 'satelliteFullIn')
			.to(cap5, { opacity: 1, duration: 3 }, 'satelliteFullIn')
			.add('lastBeat', 'satelliteFullIn+=11')
			.to(buildings, { opacity: 0, duration: 6 }, 'lastBeat')
			.to(roadsWhite, { opacity: 0, duration: 12 }, 'lastBeat')
			.to(cap5, { opacity: 0, duration: 2 }, 'lastBeat')
			.to(cap6, { opacity: 1, duration: 3 }, 'lastBeat')
			.to(cap6, { opacity: 0, duration: 6 }, 'lastBeat+=12')
			// .add('endTitle', 'lastBeat+=20')
			// .to(map, { y: '-100vh', duration: 15, ease: 'power1.in' }, 'endTitle+=5')
			// .fromTo(title, { y: '70vh' }, { y: '-150vh', duration: 15, ease: 'power1.in' }, 'endTitle')
			.to(codeLink, { opacity: 1, duration: 2 }, 'lastBeat+=20')

		return () => { 
			tl.scrollTrigger.kill();
			tl.kill();
		}
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="content-container">
		<div class="caption-box">
			<div class="caption" bind:this={cap1}>
				<p>The company's plat maps looked like official development plans.</p><p>Buyers saw lots tucked in quiet cul-de-sacs, near planned schools and shopping centers, and believed Horizon was building out the whole area.</p>
			</div>
			<div class="caption" bind:this={cap2}>
				<p>36,000 people bought <span style="color: #d68c3f; font-weight: bold;">over 100,000 lots</span>.</p>
			</div>
			<div class="caption" bind:this={cap3}>
				<p>Horizon ultimately developed one small area, around an 18-hole golf course.</p><p><span style="color: #01bfc3; font-weight: bold;">Buildings</span> went up only where <span style="color: #3083bd; font-weight: bold;">water</span> was available.</p>
			</div>
			<div class="caption" bind:this={cap4}>
				<p>Utilities and paved roads never reached the rest.</p><p><span style="color: #525263; font-weight: bold;">90,000 lots</span> have never been developed.</p>
			</div>
			<p class="caption" bind:this={cap5}>
				This is Horizon City today.
			</p>
			<p class="caption" bind:this={cap6}>
				The streets are still there, etched into the dirt.
			</p>
		</div>
		<div class="map" bind:this={map}>
			<img bind:this={satellite} src={`${base}/images/fullmap/satellite-esri.jpeg`} alt="" class="layer">
			<img
				bind:this={soldParcels}
				src={`${base}/images/fullmap/horizon-city-parcels-tan.png`}
				alt=""
				class="layer"
			/>
			
			<img
				bind:this={unbuiltParcels}
				src={`${base}/images/fullmap/sold-unbuilt-parcels-dark.png`}
				alt=""
				class="layer"
			/>
			<img bind:this={water} src={`${base}/images/fullmap/water-lines-3.svg`} alt="" class="layer" />
			<img bind:this={text} src={`${base}/images/fullmap/text.png`} alt="" class="layer" />
			<img bind:this={units} src={`${base}/images/fullmap/units.svg`} alt="" class="layer" />
			<img bind:this={roadsWhite} src={`${base}/images/fullmap/roads-white.png`} alt="" class="layer" />
			<img bind:this={roads} src={`${base}/images/fullmap/roads.svg`} alt="" class="layer" />
			
			<img
				bind:this={buildings}
				src={`${base}/images/fullmap/buildings-stroke.svg`}
				alt=""
				class="layer"
			/>
		
			<!-- <div class="key-wrapper" bind:this={keyWrapper}>
			
				<div class="key-row" bind:this={waterKey}>
					<div class="key-label">Water lines</div>
					<img src={`${base}/images/fullmap/key/water-key.svg`} class="key-line" alt="" />
				</div>
				<div class="key-row" bind:this={buildingsKey}>
					<div class="key-label">Buildings</div>
					<img src={`${base}/images/fullmap/key/buildings-key.svg`} class="key-symbol" alt="" />
				</div>
				<div class="key-row" bind:this={unbuiltKey}>
					<div class="key-label">Unbuilt lots</div>
					<img src={`${base}/images/fullmap/key/unbuilt-key.svg`} class="key-symbol" alt="" />
				</div>
			</div> -->

		</div>
		<!-- <h1 bind:this={title}>Phantom Plats</h1> -->
		<p class="code-link" bind:this={codeLink}>See the methods for this project <a href="https://github.com/var-iane/plats" target="_blank">here</a></p>
	</div>
</div>

<style>
	.wrapper {
		position: relative;
		width: 100%;
		height: 100vh;
		height: 100lvh;
		overflow: hidden;
		background-color: #fcf9f5;
	}

	.content-container {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 90vh;
		max-width: 100%;
		gap: 1.5rem;
		z-index: 0;
		/* border: 1px solid black; */
	}

	.map {
		position: relative;
		width: auto;
		flex: 1 1 0;
		min-height: 0;
		max-width: 100%;
		aspect-ratio: 5/4;
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
		/* border: 1px solid black; */
	}

	.caption-box {
		position: relative;
		flex-shrink: 0;
		width: clamp(325px, 70dvw, 750px);
		height: auto;
		min-height: 4rem;
		z-index: 3;
		/* border: 1px solid blue; */
	}

	.caption {
		position: absolute;
		top: 0;
		left: 0;
		width: clamp(325px, 80dvw, 750px);
		font-family: 'Epilogue', 'Host Grotesk', serif;
		font-weight: 300;
		font-size: clamp(1rem, 1.7vh, 1.5rem);
		line-height: 1.4;
		text-align: center;
		z-index: 3;
		opacity: 0;
		/* border: 1px solid green; */
	}

	.code-link {
		opacity: 0;
		font-size: 0.8rem;
	}

	p {
		margin: 0 0 0.25rem 0;
		text-wrap: balance;
	}

	.key-wrapper {
		position: absolute;
		top: 20%;
		left: 10%;
		z-index: 2;
		opacity: 0;
		border: 1px solid purple;
	}

	.key-row {
		display: flex;
		align-items: center;
		padding: 2px 0px;
	}

	.key-label {
		text-transform: uppercase;
		width: 120px;
		white-space: nowrap;
		font-size: 0.8rem;
	}

	.key-symbol {
		width: 20px;
		height: 10px;
	}

	.key-line {
		width: 20px;
		height: 3px;
	}

	h1 {
		font-family: 'Josefin Sans';
		font-style: italic;
		font-weight: 600;
		font-size: clamp(2rem, 20vw, 8rem);
		line-height: 1;
		color: white;
		-webkit-text-stroke: 1px black;
		position: absolute;
		bottom: 0;
		left: 50%;
		transform: translate(-50%);
		z-index: 1;
	}

</style>
