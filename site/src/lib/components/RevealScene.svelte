<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let map, soldParcels, text, units, water, buildings, unbuiltParcels, roads, satellite, title;
	let keyWrapper, soldKey, waterKey, buildingsKey, unbuiltKey;
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=6000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				// markers: true,
			}
		});

		tl.add('platMapIn', 0)
			.to(text, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(units, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(roads, { opacity: 1, duration: 3 }, 'platMapIn')
			.to(cap1, { opacity: 1, duration: 3 }, 'platMapIn')
			.add('soldIn', 'platMapIn+=7')
			.to(soldParcels, { opacity: 1, duration: 3 }, 'soldIn')
			.to(cap1, { opacity: 0, duration: 2 }, 'soldIn')
			.to(cap2, { opacity: 1, duration: 3 }, 'soldIn')
			.add('waterIn', 'soldIn+=7')
			.to(water, { opacity: 1, duration: 2 }, 'waterIn')
			.to(buildings, { opacity: 1, duration: 2 }, 'waterIn')
			.to(soldParcels, { opacity: 0, duration: 2 }, 'waterIn')
			.to(cap2, { opacity: 0, duration: 2 }, 'waterIn')
			.to(cap3, { opacity: 1, duration: 3 }, 'waterIn')
			.add('unbuiltIn', 'waterIn+=7')
			.to(unbuiltParcels, { opacity: 1, duration: 2 }, 'unbuiltIn')
			.to(cap3, { opacity: 0, duration: 2 }, 'unbuiltIn')
			.to(cap4, { opacity: 1, duration: 3 }, 'unbuiltIn')
			.add('roadsBeat', 'unbuiltIn+=7')
			.to(satellite, { opacity: 0.3, duration: 3 }, 'roadsBeat')
			.to(water, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(units, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(buildings, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(unbuiltParcels, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(text, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(cap4, { opacity: 0, duration: 2 }, 'roadsBeat')
			.to(cap5, { opacity: 1, duration: 3 }, 'roadsBeat')
			.add('satelliteFullIn', 'roadsBeat+=7')
			.to(satellite, { opacity: 1, duration: 6 }, 'satelliteFullIn')
			.to(roads, { opacity: 0, duration: 6 }, 'satelliteFullIn')
			.to(cap5, { opacity: 0, duration: 6 }, 'satelliteFullIn+=12')
			// .to(cap6, { opacity: 1, duration: 3 }, 'satelliteFullIn+=7')
			.add('endTitle', 'satelliteFullIn+=20')
			.to(map, { y: '-100vh', duration: 15, ease: 'none' }, 'endTitle')
			.fromTo(title, { y: '100vh' }, { y: '-150vh', duration: 15, ease: 'none' }, 'endTitle')

		// tl.to(keyWrapper, { opacity: 1, duration: 0.25 }, 3)
		// 	.to(keyWrapper, { opacity: 0, duration: 0.1 }, 5)

		

		return () => tl.scrollTrigger.kill();
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="content-container">
		<div class="caption-box">
			<p class="caption" bind:this={cap1}>
				The company's plat maps looked like official development plans. Buyers saw lots tucked in quiet cul-de-sacs, near planned schools and shopping centers, and believed Horizon was developing the area.
			</p>
			<p class="caption" bind:this={cap2}>
				36,000 people bought <span style="color: #731357; font-weight: bold;">over 100,000 lots</span>.
			</p>
			<p class="caption" bind:this={cap3}>
				Horizon developed one small area, around an 18-hole golf course. <span style="color: #01bfc3; font-weight: bold;">Buildings</span> went up only where the company had installed <span style="color: #3083bd; font-weight: bold;">water</span> and electricity.
			</p>
			<p class="caption" bind:this={cap4}>
				Paved roads and utilities never reached the rest, and <span style="color: #9e9a90; font-weight: bold;">90,000 lots</span> have never been developed.
			</p>
			<p class="caption" bind:this={cap5}>
				The streets are still there, etched into the dirt.
			</p>
			<p class="caption" bind:this={cap6}>
				This is what Horizon City looks like now.
			</p>
		</div>
		<div class="map" bind:this={map}>
			<img bind:this={satellite} src={`${base}/images/fullmap/satellite-esri.jpeg`} alt="" class="layer">
			<img
				bind:this={soldParcels}
				src={`${base}/images/fullmap/horizon-city-parcels.png`}
				alt=""
				class="layer"
			/>
			
			<img
				bind:this={unbuiltParcels}
				src={`${base}/images/fullmap/sold-unbuilt-parcels-1.png`}
				alt=""
				class="layer"
			/>
			<img bind:this={water} src={`${base}/images/fullmap/water-lines-3.svg`} alt="" class="layer" />
			<img bind:this={text} src={`${base}/images/fullmap/text.svg`} alt="" class="layer" />
			<img bind:this={units} src={`${base}/images/fullmap/units.svg`} alt="" class="layer" />
			<img bind:this={roads} src={`${base}/images/fullmap/roads.svg`} alt="" class="layer" />
			<img
				bind:this={buildings}
				src={`${base}/images/fullmap/buildings-stroke.svg`}
				alt=""
				class="layer"
			/>
		
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
					<div class="key-label">Unbuilt lots</div>
					<img src={`${base}/images/fullmap/key/unbuilt-key.svg`} class="key-symbol" alt="" />
				</div>
			</div>

		</div>
		<h1 bind:this={title}>Phantom Plats</h1>
	</div>
</div>

<style>
	.wrapper {
		position: relative;
		width: 100%;
		height: 100vh;
		height: 100lvh;
		overflow: hidden;
		background-color: #eee9e8;
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
		width: clamp(325px, 70dvw, 700px);
		height: auto;
		min-height: 4rem;
		z-index: 3;
		/* border: 1px solid blue; */
	}

	.caption {
		position: absolute;
		top: 0;
		left: 0;
		width: clamp(325px, 70dvw, 700px);
		font-family: 'Epilogue', 'Host Grotesk', serif;
		font-weight: 300;
		line-height: 1.3;
		text-align: center;
		text-wrap: balance;
		padding: 6px;
		z-index: 3;
		opacity: 0;
		/* border: 1px solid green; */
	}

	/* .caption-box {
		position: absolute;
		left: 50%;
		width: clamp(150px, 30dvw, 450px);
		padding: 6px;
		z-index: 3;
		background-color: #cee0dd;
		border: 1px solid black;
		border-radius: 8px;
		font-weight: 300;
	} */


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
