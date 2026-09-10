<script>
	import { base } from '$app/paths';

	let items = [
		{
			title: 'New York City',
			lots: 'Horizon City Estates, lots 27-33',
			image: `${base}/images/zooms/nyc-west2.png`
		},
		{
			title: 'Chicago',
			lots: 'Horizon City Estates, lot 73',
			image: `${base}/images/zooms/chicago-west2.png`
		},
		{
			title: 'Phoenix',
			lots: 'Horizon City Estates, lot 68',
			image: `${base}/images/zooms/phoenix-transparent.png`
		},
		{
			title: 'Cleveland',
			lots: 'Shadow Ridge, lots 8-14',
			image: `${base}/images/zooms/cleveland.png`
		},
		{
			title: 'Germany',
			lots: 'Shadow Ridge, lots 3, 6, 15, 17, 34',
			image: `${base}/images/zooms/germany.png`
		},
		{
			title: 'Portland',
			lots: 'Horizon City Estates, lot 59',
			image: `${base}/images/zooms/portland.png`
		},
		{
			title: 'Birmingham',
			lots: 'Horizon City Estates, lot 55',
			image: `${base}/images/zooms/birmingham.png`
		},
		{ title: 'Seattle', image: `${base}/images/zooms/seattle.png` },
		{
			title: 'Minneapolis',
			lots: 'Horizon City, lots 81, 82',
			image: `${base}/images/zooms/minneapolis.png`
		},
		{
			title: 'Canada',
			lots: 'Mountain Vista, lots 5, 6',
			image: `${base}/images/zooms/canada2.png`
		}
	];

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

	// let activeId = $state(horizonCityEstates[null].id);

	// let activeItem = $derived(items.find((item) => item.id === activeId));

</script>

<div class="wrapper">

	<div class="sticky-header">
		<h2>A city of cities</h2>
		<hr class="full-bleed-line">
	</div>
	<p>
		Of the roughly 39,000 people who bought parcels, only 11% resided within 100 miles of Horizon City at the time. A full 80% of owners lived at least 500 miles away—not exactly "locals".
	<br><br>
		Mini-neighborhoods, like New New York or Mini-Minneapolis, Whether because door-to-door salesmen sold one lot at a time, regional preferences, or people
		knowing others who bought nearby,
	</p>
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
	<div class="subdivision">
		<h3>Shadow Ridge subdivision</h3>
		<img
			class="legend"
			src={`${base}/images/zooms/shadow-ridge.png`}
			alt="Location of Shadow Ridge subdivision"
		/>
		<div class="image-grid">
			{#each shadowRidge as item (item.title)}
				<figure class="shadow-ridge">
					<p class="city">{item.title}</p>
					<p class="lots">{item.lots}</p>
					<img src={item.image} alt={`Map showing parcels owned by residents of ${item.title}`} />
				</figure>
			{/each}
		</div>
	</div>

	<div class="subdivision">
		<h3>Mountain Vista subdivision</h3>
		<div class="image-grid">
		<img
			class="legend"
			src={`${base}/images/zooms/mountain-vista.png`}
			alt="Location of Mountain Vista subdivision"
		/>
		
			{#each mountainVista as item (item.title)}
				<figure class="mountain-vista">
					<p class="city">{item.title}</p>
					<p class="lots">{item.lots}</p>
					<img src={item.image} alt={`Map showing parcels owned by residents of ${item.title}`} />
				</figure>
			{/each}
		</div>
	</div>

	<!-- TODO: horizon city estates overlay... -->
	<div class="subdivision">
		<h3>Horizon City Estates subdivision</h3>
		<img
			class="legend"
			src={`${base}/images/zooms/horizon-city-estates.png`}
			alt="Location of Horizon City Estates subdivision"
		/>
		<!-- <div class="city-buttons">
			{#each horizonCityEstates as item (item.id)}
				<button
					class="city-button"
					class:active={item.id === activeId}
					onclick={() => (activeId = item.id)}
				>
				{item.title}
				</button>
			{/each}
		</div>
		<div class="image-box">
			{#if activeItem}
				<img src={activeItem.image} alt={`Map showing parcels owned by residents of ${activeItem.title}`} />
			{/if}
		</div> -->
	</div>
	<div class="image-grid">
			{#each horizonCityEstates as item (item.title)}
				<figure class="horizon-city-estates">
					<p class="city">{item.title}</p>
					<p class="lots">{item.lots}</p>
					<img src={item.image} alt={`Map showing parcels owned by residents of ${item.title}`} />
				</figure>
			{/each}
		</div>
</div>

<style>
	.wrapper {
		--viewport-padding: 16px;
		display: grid;
		grid-template-columns: 1fr min(42rem, calc(100% - var(--viewport-padding) * 2)) 1fr;
		gap: 0 var(--viewport-padding);
		padding: 20px 0;
		background-color: #e7eddd;
	}

	.wrapper > * {
		grid-column: 2;
	}

	.full-bleed {
		width: 100%;
		grid-column: 1 / -1;
	}

	.full-bleed-line {
		width: 100vw;
		position: relative;
		left: 50%;
		transform: translateX(-50%);
		border: none;
		border-top: 0.5px solid black;
		margin: 1rem 0 0 0;
	}

	.sticky-header {
		position: sticky;
		top: 0;
		z-index: 2;
		background-color: inherit;
		padding: 1rem 0 0 0;
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
		/* padding-top: 1rem; */
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

	.mountain-vista img {
		width: 80px;
	}

	.shadow-ridge img {
		width: 250px;
	}

	.horizon-city-estates img {
		width: 250px;
	}

	.text {
		max-width: 1000px;
		text-align: center;
		padding: 20px 0;
	}
</style>
