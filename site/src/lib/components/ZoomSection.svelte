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
		{ title: 'Canada', lots: 'Lots 5, 6', image: `${base}/images/zooms/mountain-vista-canada.png` },
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
				end: '+=3000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				invalidateOnRefresh: true
			}
		});

		tl.to(subdivision, { opacity: 1 }, 6)
	});

</script>

<div class="wrapper" bind:this={pinnedWrapper}>

	<h2>Artificial enclaves</h2>
		
	<div class="intro">
		<p>Why the clustering?</p>
		<p>Sales reps were given a limited batch of inventory to sell at a time. Horizon had sales offices across the U.S. and abroad, and a rep's territory might influence who had access to which lots.</p>
		<p>A rep might open an envelope at a dinner party — "these are tonight's lots!" — and warn attendees that they could be gone by morning.</p>
		<p>
			Zoom into a single subdivision, and the .
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
	<div class="subdivision" bind:this={subdivision}>

		<div class="shadow-ridge" bind:this={shadowRidgeBeat}>
			<h3>Shadow Ridge subdivision</h3>
			<img
				class="legend"
				src={`${base}/images/zooms/shadow-ridge.png`}
				alt="Location of Shadow Ridge subdivision"
			/>
			<img
				class="legend"
				src={`${base}/images/zooms/subdivision-enclaves-background_shadow-ridge.png`}
				alt="Enclaves in Shadow Ridge"
			/>
			<!-- <div class="image-grid">
				{#each shadowRidge as item (item.title)}
					<figure class="shadow-ridge">
						<p class="city">{item.title}</p>
						<p class="lots">{item.lots}</p>
						<img src={item.image} alt={`Map showing parcels owned by residents of ${item.title}`} />
					</figure>
				{/each}
			</div> -->
		</div>
	
		<div class="mountain-vista" bind:this={mountainVistaBeat}>
			<h3>Mountain Vista subdivision</h3>
			<div class="image-grid">
			<img
				class="legend"
				src={`${base}/images/zooms/mountain-vista.png`}
				alt="Location of Mountain Vista subdivision"
			/>
			<img
				class="legend"
				src={`${base}/images/zooms/subdivision-enclaves-background_mountain-vista.png`}
				alt="Enclaves in Mountain Vista"
			/>
			
				<!-- {#each mountainVista as item (item.title)}
					<figure class="mountain-vista">
						<p class="city">{item.title}</p>
						<p class="lots">{item.lots}</p>
						<img src={item.image} alt={`Map showing parcels owned by residents of ${item.title}`} />
					</figure>
				{/each} -->
			</div>
		</div>

		<div class="horizon-city-estates" bind:this={horizonCityEstatesBeat}>
			<h3>Horizon City Estates subdivision</h3>
			<img
				class="legend"
				src={`${base}/images/zooms/horizon-city-estates.png`}
				alt="Location of Horizon City Estates subdivision"
			/>
			<img
					class="legend"
					src={`${base}/images/zooms/subdivision-enclaves-background_horizon-city-estates.png`}
					alt="Enclaves in Horizon City Estates"
				/>
		</div>
	</div>
</div>

<style>
	.wrapper {
		--viewport-padding: 16px;
		display: grid;
		grid-template-columns: 1fr min(42rem, calc(100% - var(--viewport-padding) * 2)) 1fr;
		gap: 0 var(--viewport-padding);
		padding: 20px 0;
		background-color: #ca6e56;
	}

	.wrapper > * {
		grid-column: 2;
	}

	.full-bleed {
		width: 100%;
		grid-column: 1 / -1;
	}

	/* .full-bleed-line {
		width: 100vw;
		position: relative;
		left: 50%;
		transform: translateX(-50%);
		border: none;
		border-top: 0.5px solid black;
		margin: 1rem 0 0 0;
	} */

	/* .sticky-header {
		position: sticky;
		top: 0;
		z-index: 2;
		background-color: inherit;
		padding: 1rem 0 0 0;
	} */

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
		padding-top: 1rem;
	}

	.city {
		font-size: 0.9rem;
		font-weight: 400;
	}

	.lots {
		font-size: 0.8rem;
		font-weight: 300;
	}

	.subdivision {
		padding: 20px 0;
		opacity: 0;
	}

	.image-grid {
		/* display: grid;
        grid-template-columns: repeat(auto-fit, minmax(min(200px, 100%), 1fr));
        gap: 1rem 0.2rem;
		padding: 20px 0; */
		display: flex;
		gap: 1rem;
		align-items: flex-start;
		flex-wrap: wrap;
	}

	.image {
		display: flex;
		align-items: flex-start;
		/* flex-direction: column; */
		/* gap: 0.5rem; */
	}

	.image img {
		height: 300px;
		width: auto;
		/* width: 50%;
		height: auto; */
		/* aspect-ratio: 1 / 1; */
		/* object-fit: cover; */
		max-width: 100%;
		border: 1px solid black;
		background-color: #ffffff;
	}

	.legend {
		width: 100%;
		min-width: 300px;
		max-width: 450px;
	}

	img {
		border: 1px solid black;
	}

	.shadow-ridge img {
		width: 250px;
	}


	.mountain-vista img {
		width: 80px;
	}

	
	.horizon-city-estates img {
		width: 250px;
	}
</style>
