<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);

	let pinnedWrapper;
	let allParcels, water, buildings, unbuiltParcels, roads, satellite;
	let keyWrapper, soldKey, waterKey, buildingsKey, unbuiltKey;
	let cap1, cap2, cap3, cap4;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=6000',
				pin: true,
				scrub: 3,
				anticipatePin: 1,
				markers: true,
				ease: 'none',
			}
		});

		tl.to(allParcels, { opacity: 1, duration: 0 }, 0)
			.to(water, { opacity: 1, duration: 0.25 }, 1)
			.to(allParcels, { opacity: 0.1, duration: 0.2 }, '<')
			.to(buildings, { opacity: 1, duration: 0.5 }, 2)
			.to(allParcels, { opacity: 0, duration: 0.1 }, '<')
			.to(unbuiltParcels, { opacity: 1, duration: 0.5 }, 2.5)
			.to(satellite, { opacity: 0.2, duration: 0.5 }, 5)
			.to(water, { opacity: 0, duration: 0.25 }, 5)
			.to(roads, { opacity: 1, duration: 0.25 }, 5)
			.to(satellite, { opacity: 1, duration: 2 }, 5)
			.to(buildings, { opacity: 0, duration: 0.5 }, 6)
			.to(unbuiltParcels, { opacity: 0, duration: 0.5 }, 6)
			.to(roads, { opacity: 0, duration: 0.5 }, 6);

		// tl.to(soldKey, { opacity: 1, duration: 0 }, 0)
		// 	.to(waterKey, { opacity: 1, duration: 0.25 }, '>')
		// 	.to(buildingsKey, { opacity: 1, duration: 0.25 }, '>')
		// 	.to(unbuiltKey, { opacity: 1, duration: 0.25 }, '>');

		tl.to(keyWrapper, { opacity: 1, duration: 0.25 }, 3)
			.to(keyWrapper, { opacity: 0, duration: 0.1 }, 5)

		tl.fromTo(cap1, { y: '100svh' }, { y: '-30svh', duration: 1 }, 0)
			.fromTo(cap2, { y: '100svh' }, { y: '-30svh', duration: 1 }, 1)
			.fromTo(cap3, { y: '100svh' }, { y: '2svh', duration: 1 }, 2)
			.to(cap3, { opacity: 0, duration: 0.5 }, 3.5)
			.fromTo(cap4, { opacity: 0, y: '2svh' }, { opacity: 1, y: '2svh', duration: 0.25 }, 7);

		return () => tl.scrollTrigger.kill();
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<p class="caption-box" bind:this={cap1}>
		Nearly 100,000 <span style="color: #731357; font-weight: bold;">parcels</span> were sold to over 36,000 individuals around the world.
	</p>
	<p class="caption-box" bind:this={cap2}>
		There was one problem. <br><br> <span style="color: #3083bd; font-weight: bold;">Water lines</span> never reached most of the lots.
	</p>
	<p class="caption-box" bind:this={cap3}>
		<span style="color: #01bfc3; font-weight: bold;">Buildings</span> sprung up where water was available, but the <span style="color: #9e9a90; font-weight: bold;">rest of the parcels</span> were never built on.
	</p>
	<p class="caption-box" bind:this={cap4}>
		This is what Horizon City looks like now.
	</p>
	<div class="map">
		<img
			bind:this={allParcels}
			src={`${base}/images/fullmap/horizon-city-parcels.png`}
			alt=""
			class="layer"
		/>
		<img bind:this={satellite} src={`${base}/images/fullmap/satellite-esri.jpeg`} alt="" class="layer">
		<img
			bind:this={unbuiltParcels}
			src={`${base}/images/fullmap/sold-unbuilt-parcels-1.png`}
			alt=""
			class="layer"
		/>
		<img bind:this={water} src={`${base}/images/fullmap/water-lines-3.svg`} alt="" class="layer" />
		<img
			bind:this={buildings}
			src={`${base}/images/fullmap/buildings-stroke.svg`}
			alt=""
			class="layer"
		/>
		<img bind:this={roads} src={`${base}/images/fullmap/roads-white.png`} alt="" class="layer" />
		<div class="key-wrapper" bind:this={keyWrapper}>
			<!-- <div class="key-row" bind:this={soldKey}>
				<div class="key-label">Sold parcels</div>
				<img src={`${base}/images/fullmap/key/sold-key.svg`} class="key-symbol" alt="" />
			</div> -->
			<div class="key-row" bind:this={waterKey}>
				<div class="key-label">Water lines</div>
				<img src={`${base}/images/fullmap/key/water-key.svg`} class="key-line" alt="" />
			</div>
			<div class="key-row" bind:this={buildingsKey}>
				<div class="key-label">Buildings</div>
				<img src={`${base}/images/fullmap/key/buildings-key.svg`} class="key-symbol" alt="" />
			</div>
			<div class="key-row" bind:this={unbuiltKey}>
				<div class="key-label">Unbuilt parcels</div>
				<img src={`${base}/images/fullmap/key/unbuilt-key.svg`} class="key-symbol" alt="" />
			</div>
		</div>
	</div>
</div>

<style>
	.wrapper {
		position: relative;
		width: 100%;
		height: 100dvh;
		overflow: hidden;
		background-color: #e8e5de;
	}

	.map {
		position: absolute;
		/* inset: 0; */
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: auto;
		height: 100%;
		aspect-ratio: 5/4;
		max-width: 100%;
		max-height: 100%;
		/* border: 1px solid black; */
		z-index: 0;
	}

	.caption-box {
		position: absolute;
		left: 50%;
		width: clamp(150px, 30dvw, 450px);
		padding: 6px;
		z-index: 3;
		background-color: #cee0dd;
		border: 1px solid black;
		border-radius: 8px;
		font-weight: 300;
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

	.key-wrapper {
		position: absolute;
		top: 20%;
		left: 10%;
		z-index: 2;
		opacity: 0;
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

	.key-symbol {
		width: 20px;
		height: 10px;
	}

	.key-line {
		width: 20px;
		height: 3px;
	}
</style>
