<script>
	import { onMount } from 'svelte';
	import { base } from '$app/paths';
	import * as d3 from 'd3';

	// let { activeClusters = [], clusterColors } = $props();

	let container;
	let canvas;
	let parcelData = $state(null);
	let width = $state(0);
	let height = $state(0);
	let projection = $state(null);

	onMount(async () => {
		const response = await fetch(`${base}/data/us_owners_parcels_clustered_viz.geojson`);
		parcelData = await response.json();
	});

    $effect(() => {
        if (parcelData && width && height) {
            projection = d3.geoMercator().fitSize([width, height], parcelData);
        }
    });

    $effect(() => {
        if (parcelData && projection && canvas) {
            draw();
        }
    })

    function draw() {
        const ctx = canvas.getContext('2d');
        const pathGenerator = d3.geoPath(projection, ctx);

        ctx.clearRect(0, 0, width, height);

        for (const feature of parcelData.features) {
            ctx.beginPath();
            pathGenerator(feature);
            ctx.fillStyle = '#e0e0e0';
            ctx.fill()
        }
    }
</script>

<div class='map-container' bind:this={container} bind:clientWidth={width} bind:clientHeight={height}>
    <canvas bind:this={canvas} {width} {height}></canvas>
</div>

<style>
	.map-container {
        width: 800px;
		/* width: min(90vw, 800px); */
		aspect-ratio: 1 / 1;
		overflow: hidden;
		/* width: 600px;
        height: 400px; */
		/* width: 100%;
        aspect-ratio: 3 / 2; */
	}

</style>