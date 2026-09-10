<script>
	import { onMount } from 'svelte';
	import { base } from '$app/paths';
	import * as d3 from 'd3';

	let { activeClusters = [], clusterColors, onClusterClick } = $props();

	let container;
	let statesData = $state(null);
	let ownersData = $state(null);
	let width = $state(0);
	let height = $state(0);
	let projection = $state(null);

	let pathGenerator = $derived(projection ? d3.geoPath(projection) : null);

	onMount(async () => {
        const [statesResponse, ownersResponse] = await Promise.all([
            fetch(`${base}/data/us_states.geojson`),
            fetch(`${base}/data/unique_us_owners_points_clustered_viz.geojson`)
        ]);
        statesData = await statesResponse.json();
        ownersData = await ownersResponse.json();
	});

	$effect(() => {
		if (statesData && width && height) {
			projection = d3.geoAlbersUsa().fitSize([width, height], statesData);
		}
	});
</script>

<div
	class="map-container"
	bind:this={container}
	bind:clientWidth={width}
	bind:clientHeight={height}
>
	<svg {width} {height}>
		{#if pathGenerator}
			{#each statesData.features as feature (feature.properties.STATEFP)}
				<path d={pathGenerator(feature)} class="state" />
			{/each}
		{/if}

		{#if projection && ownersData}
			{#each ownersData.features as feature, i (i)}
				<!-- a temp guard against US territory null coordinates from geoAlbersUsa -->
				{@const projected = projection(feature.geometry.coordinates)}
				{#if projected}
					{@const [x, y] = projected}
					<circle cx={x} cy={y} r="1" class="owner-point" />
				{/if}
			{/each}
		{/if}
	</svg>
</div>

<style>
	.map-container {
		width: min(90vw, 800px);
		aspect-ratio: 3 / 2;
		overflow: hidden;
		/* width: 600px;
        height: 400px; */
		/* width: 100%;
        aspect-ratio: 3 / 2; */
	}

	svg {
		display: block;
		/* width: 100%;
		height: 100%; */
	}
	.state {
		fill: #e8e8e8;
		stroke: #ffffff;
		stroke-width: 1;
	}
	.owner-point {
		fill: #999;
	}
</style>
