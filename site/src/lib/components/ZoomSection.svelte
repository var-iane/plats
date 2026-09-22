<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let subdivision;
	let shadowRidgeBeat, mountainVistaBeat, horizonCityEstatesBeat;

	let shadowRidge = [
		{
			title: 'Cleveland',
			lots: 'Lots 8-14',
			image: `${base}/images/zooms/shadow-ridge-cleveland.png`
		},
		{
			title: 'Germany',
			lots: 'Lots 3, 6, 15, 17, 34',
			image: `${base}/images/zooms/shadow-ridge-germany.png`
		}
	];

	let mountainVista = [
		{
			title: 'Las Vegas',
			lots: 'Lots 4, 7',
			image: `${base}/images/zooms/mountain-vista-lasvegas.png`
		},
		{ title: 'Canada', lots: 'Lots 5, 6', image: `${base}/images/zooms/mountain-vista-canada.png` }
	];

	let horizonCityEstates = [
		{
			id: 'nyc',
			title: 'New York City',
			lots: 'Lots 27-33',
			image: `${base}/images/zooms/horizon-city-estates-nyc.png`
		},
		{
			id: 'chi',
			title: 'Chicago',
			lots: 'Lot 73',
			image: `${base}/images/zooms/horizon-city-estates-chicago.png`
		},
		{
			id: 'phx',
			title: 'Phoenix',
			lots: 'Lot 68',
			image: `${base}/images/zooms/horizon-city-estates-phoenix.png`
		},
		{
			id: 'port',
			title: 'Portland',
			lots: 'Lot 59',
			image: `${base}/images/zooms/horizon-city-estates-portland.png`
		},
		{
			id: 'bham',
			title: 'Birmingham',
			lots: 'Lot 55',
			image: `${base}/images/zooms/horizon-city-estates-birmingham.png`
		}
	];

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=1000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				invalidateOnRefresh: true
			}
		});

		tl.to(subdivision, { opacity: 1 }, 6);
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	
	<div class="intro">
		<h2>Artificial enclaves</h2>
		<p>Why the clustering?</p>
		<p>
			Sales reps were given a limited batch of inventory to sell at a time — say, certain blocks
			within a specific unit of a subdivision. Horizon had sales offices across the U.S. and abroad,
			and a rep's territory influenced who could buy where.
		</p>
		<p>
			At sales dinner parties, reps were known to open envelopes revealing that night's lots and
			warn attendees that they could be gone by morning.
		</p>
		<p>
			These tactics likely produced the artificial enclaves, like a mini-Minneapolis or New New
			York, visible in the ownership data.
		</p>
	</div>

	<!-- <div class="image-grid">
		{#each items as item (item.title)}
			<figure class="image">
				<p class="city">{item.title}</p>
				<p class="lots">{item.lots}</p>
				<img 
					src={item.image}
					alt={`Map showing parcels owned by residents of ${item.title}`}
				/>
			</figure>
		{/each}
	</div> -->

	<div class="examples">

		<h3>Shadow Ridge subdivision</h3>
		<figure class="example shadow-ridge">
			<img
				class="locator"
				src={`${base}/images/zooms/shadow-ridge.png`}
				alt="Location of Shadow Ridge subdivision"
			/>
			<div class="zoom-box">
				<img
					class="zoom"
					src={`${base}/images/zooms/subdivision-enclaves_shadow-ridge.png`}
					alt="Parcels in Shadow Ridge colored by owner residence"
				/>
				<div class="key">
					<p class="chip"><span style="color: #2f8ac4; font-weight: 500;">Cleveland:</span> Lots 8-14</p>
					<p class="chip"><span style="color: #ff6b5a; font-weight: 500;">North Rhine-Westphalia, Germany:</span> Lots 3, 6, 15, 17, 34</p>
				</div>
			</div>
			
		</figure>

		<h3>Mountain Vista subdivision</h3>
		<figure class="example mountain-vista">
			<img
				class="locator"
				src={`${base}/images/zooms/mountain-vista.png`}
				alt="Location of Mountain Vista subdivision"
			/>
			<div class="zoom-box">
				<img
					class="zoom"
					src={`${base}/images/zooms/subdivision-enclaves-background_mountain-vista.png`}
					alt="Parcels in Mountain Vista colored by owner residence"
				/>
				<div class="key-wrapper">
					<div class="key-row"><span style="color: #3a3b78; font-weight: 500;">Las Vegas:</span> Lots 4, 7</div>
					<div class="key-row"><span style="color: #1ebecf; font-weight: 500;">British Columbia, Canada:</span> Lots 5, 6</div>
				</div>
			</div>
		</figure>

		<h3>Horizon City Estates subdivision</h3>
		<figure class="example horizon-city-estates">
			<img
				class="locator"
				src={`${base}/images/zooms/horizon-city-estates.png`}
				alt="Location of Horizon City Estates subdivision"
			/>
			<div class="zoom-box">
				<img
					class="zoom"
					src={`${base}/images/zooms/subdivision-enclaves-background_horizon-city-estates.png`}
					alt="Parcels in Horizon City Estates colored by owner residence"
				/>
				<div class="key">
					<p class="chip"><span style="color: #d326be; font-weight: 500;">Birmingham:</span> Lot 55</p>
					<p class="chip"><span style="color: #9966cc; font-weight: 500;">Portland:</span> Lot 59</p>
					<p class="chip"><span style="color: #e73f74; font-weight: 500;">Chicago:</span> Lot 73</p>
					<p class="chip"><span style="color: #94a800; font-weight: 500;">Phoenix:</span> Lot 68</p>
					<p class="chip"><span style="color: #ffa600; font-weight: 500;">New York City:</span> Lots 27-33</p>
				</div>
			</div>
		</figure>
	</div>
</div>

<style>
	.wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #ca6e56;
		/* --viewport-padding: 16px;
		display: grid;
		grid-template-columns: 1fr min(42rem, calc(100% - var(--viewport-padding) * 2)) 1fr;
		gap: 0 var(--viewport-padding);
		padding: 20px 0;
		background-color: #ca6e56; */
	}

	.wrapper > * {
		/* grid-column: 2; */
	}

	.full-bleed {
		width: 100%;
		grid-column: 1 / -1;
	}

	h2 {
		font-family: 'Epilogue', sans-serif;
		/* padding: 6px 0; */
	}

	h3 {
		font-family: 'Epilogue', sans-serif;
		font-weight: 600;
		padding: 6px 0;
	}

	p {
		font-family: 'Host Grotesk', 'Epilogue', sans-serif;
		font-weight: 300;
	}

	.intro p {
		padding-top: 1rem;
	}

	.intro {
		max-width: 42rem;
	}

	.examples {
		--scale: 0.613; /* to make widest image fit max column width */

		max-width: 63rem;
		margin: 0 auto;
		padding: 20px 0px;
	}

	.example {
		/* display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 1rem 0.2rem;
		padding: 20px 0; */
		display: flex;
		gap: 1rem;
		align-items: flex-start;
		flex-wrap: wrap;
	}

	.shadow-ridge img.zoom {
		width: calc(495px * var(--scale));
	}
	.mountain-vista img.zoom {
		width: calc(173px * var(--scale));
	}
	.horizon-city-estates img.zoom {
		width: calc(1094px * var(--scale));
	}

	.locator {
		width: 100%;
		min-width: 300px;
		max-width: 450px;
		border: 1px solid black;
		display: block;
		margin-bottom: 1rem;
	}

	.zoom-box {
		/* position: relative; */
		display: flex;
		/* min-width: 300px;
		max-width: 350px; */
		background-color: #eee9e8;
		border: 1px solid black;
	}

	.zoom {
		/* height: auto;
		display: block;
		max-width: 100%; */
		/* border: 1px solid black; */
	}

	.key { 
		position: absolute;
		top: 0.5rem;
		right: 0.5rem;
		display: flex;
		flex-wrap: wrap;
		
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
		/* opacity: 0; */
	}

	.key-label {
		text-transform: uppercase;
		width: 120px;
		white-space: nowrap;
		font-size: 0.8rem;
	}

	.chip {
		font-family: 'Host Grotesk', sans-serif;
		font-size: 1rem;
		font-weight: 500;
		white-space: nowrap;
		gap: 1rem;
		/* display: inline-block;
		width: 0.75rem;
		height: 0.75rem;
		margin-right: 0.5rem;
		border: 1px solid rgba(0, 0, 0, 0.3);
		vertical-align: baseline;
		flex-shrink: 0; */
	}

	@media (max-width: 720px) {
		.examples {
			--scale: 0.45;
		}
	}
</style>
