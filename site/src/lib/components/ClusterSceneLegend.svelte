<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let units,
		nycParcels,
		chicagoParcels,
		clevelandParcels,
		seattleParcels,
		portlandParcels,
		phoenixParcels,
		minneapolisParcels,
		birminghamParcels,
		stlouisParcels,
		lasvegasParcels,
		otherParcels,
		internationalParcels;
	let usMap,
		nyc,
		chicago,
		cleveland,
		seattle,
		portland,
		phoenix,
		minneapolis,
		birmingham,
		stlouis,
		lasvegas,
		other,
		international;
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7, cap8, cap9, cap10, cap11, cap12, cap13;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=3000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				markers: true
			}
		});

		tl.to(units, { opacity: 1, duration: 0.5 }, 0)
			.to(nycParcels, { opacity: 1, duration: 0.5 }, '>')
			.to(chicagoParcels, { opacity: 1, duration: 0.5 }, '>')
			.to(clevelandParcels, { opacity: 1, duration: 0.5 }, '>')
			.to(seattleParcels, { opacity: 1, duration: 0.5 }, '>')
			.to(portlandParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(phoenixParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(minneapolisParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(birminghamParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(stlouisParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(lasvegasParcels, { opacity: 1, duration: 0.25 }, '>')
			.to(otherParcels, { opacity: 1, duration: 0.25 }, '>')
			.to({}, { duration: 2 })
			.to(internationalParcels, { opacity: 1, duration: 0.25 }, '>');

		tl.to(usMap, { opacity: 1, duration: 0.5 }, 0)
			.to(nyc, { opacity: 1, duration: 0.5 }, '>')
			.to(chicago, { opacity: 1, duration: 0.5 }, '>')
			.to(cleveland, { opacity: 1, duration: 0.5 }, '>')
			.to(seattle, { opacity: 1, duration: 0.5 }, '>')
			.to(portland, { opacity: 1, duration: 0.25 }, '>')
			.to(phoenix, { opacity: 1, duration: 0.25 }, '>')
			.to(minneapolis, { opacity: 1, duration: 0.25 }, '>')
			.to(birmingham, { opacity: 1, duration: 0.25 }, '>')
			.to(stlouis, { opacity: 1, duration: 0.25 }, '>')
			.to(lasvegas, { opacity: 1, duration: 0.25 }, '>')
			.to(other, { opacity: 1, duration: 0.25 }, '>');

		tl.to(cap1, { opacity: 1, duration: 0.5 }, 0)
			.to(cap2, { opacity: 1, duration: 0.5 }, '>')
			.to(cap3, { opacity: 1, duration: 0.5 }, '>')
			.to(cap4, { opacity: 1, duration: 0.5 }, '>')
			.to(cap5, { opacity: 1, duration: 0.5 }, '>')
			.to(cap6, { opacity: 1, duration: 0.25 }, '>')
			.to(cap7, { opacity: 1, duration: 0.25 }, '>')
			.to(cap8, { opacity: 1, duration: 0.25 }, '>')
			.to(cap9, { opacity: 1, duration: 0.25 }, '>')
			.to(cap10, { opacity: 1, duration: 0.25 }, '>')
			.to(cap11, { opacity: 1, duration: 0.25 }, '>')
			.to(cap12, { opacity: 1, duration: 0.25 }, '>');

		return () => tl.scrollTrigger.kill();
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="cell owner-cell">
		<div class="frame owner-frame">
			<p class="map-label">Where owners lived</p>
			<img
				bind:this={usMap}
				src={`${base}/images/owner-clusters/basemap.svg`}
				alt=""
				class="layer"
			/>
			<img bind:this={nyc} src={`${base}/images/owner-clusters/nyc.svg`} alt="" class="layer" />
			<img
				bind:this={chicago}
				src={`${base}/images/owner-clusters/chicago.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={cleveland}
				src={`${base}/images/owner-clusters/cleveland.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={seattle}
				src={`${base}/images/owner-clusters/seattle.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={portland}
				src={`${base}/images/owner-clusters/portland.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={phoenix}
				src={`${base}/images/owner-clusters/phoenix.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={minneapolis}
				src={`${base}/images/owner-clusters/minneapolis.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={birmingham}
				src={`${base}/images/owner-clusters/birmingham.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={stlouis}
				src={`${base}/images/owner-clusters/stlouis.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={lasvegas}
				src={`${base}/images/owner-clusters/lasvegas.svg`}
				alt=""
				class="layer"
			/>
			<img bind:this={other} src={`${base}/images/owner-clusters/other.png`} alt="" class="layer" />
		</div>
	</div>

	<div class="legend">
		<p bind:this={cap1} class="lede">
			80% of buyers resided at least 500 miles away. They lived in:
		</p>
		<p bind:this={cap2} style="color: #ffa100" class="caption">New York City</p>
		<p bind:this={cap3} style="color: #e73f74" class="caption">Chicago</p>
		<p bind:this={cap4} style="color: #2f8ac4" class="caption">Cleveland</p>
		<p bind:this={cap5} style="color: #11a579" class="caption">Seattle</p>
		<p bind:this={cap6} style="color: #9966cc" class="caption">Portland</p>
		<p bind:this={cap7} style="color: #94a800" class="caption">Phoenix</p>
		<p bind:this={cap8} style="color: #6666cc" class="caption">Minneapolis</p>
		<p bind:this={cap9} style="color: #d326be" class="caption">Birmingham</p>
		<p bind:this={cap10} style="color: #1ebecf" class="caption">St. Louis</p>
		<p bind:this={cap11} style="color: #3a3b78" class="caption">Las Vegas</p>
		<p bind:this={cap12} style="color: #b3b3b3" class="caption">and all over the U.S.</p>
		<p bind:this={cap13} style="color: #ff6b5a" class="caption">Many bought from</p>
	</div>

	<div class="cell parcel-cell">
		<div class="frame parcel-frame">
			<p class="map-label">Where they bought parcels</p>
			<img
				bind:this={units}
				src={`${base}/images/parcel-clusters/units-filled-white.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={nycParcels}
				src={`${base}/images/parcel-clusters/nyc.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={chicagoParcels}
				src={`${base}/images/parcel-clusters/chicago.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={clevelandParcels}
				src={`${base}/images/parcel-clusters/cleveland.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={seattleParcels}
				src={`${base}/images/parcel-clusters/seattle.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={portlandParcels}
				src={`${base}/images/parcel-clusters/portland.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={phoenixParcels}
				src={`${base}/images/parcel-clusters/phoenix.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={minneapolisParcels}
				src={`${base}/images/parcel-clusters/minneapolis.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={birminghamParcels}
				src={`${base}/images/parcel-clusters/birmingham.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={stlouisParcels}
				src={`${base}/images/parcel-clusters/stlouis.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={lasvegasParcels}
				src={`${base}/images/parcel-clusters/lasvegas.svg`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={otherParcels}
				src={`${base}/images/parcel-clusters/other.png`}
				alt=""
				class="layer"
			/>
			<img
				bind:this={internationalParcels}
				src={`${base}/images/parcel-clusters/international.png`}
				alt=""
				class="layer"
			/>
		</div>
	</div>
</div>

<style>
	.wrapper {
		--ratio-owner: 1.4808;
		--ratio-parcel: 1.25;

		position: relative;
		width: 100%;
		height: 100vh;
		height: 100lvh;
		overflow: hidden;
		box-sizing: border-box;
		padding: clamp(0.5rem, 2vh, 1.25rem);
		gap: clamp(0.5rem, 2vh, 1.25rem);
		font-family: 'Epilogue', sans-serif;

		display: grid;
		align-content: center;
		grid-template:
			'owner' 1fr
			'legend' auto
			'parcel' 1fr / minmax(0, 1fr);
	}

	@media (min-aspect-ratio: 1/1) {
		.wrapper {
			grid-template:
				'legend legend' auto / minmax(0, 1.48fr) minmax(0, 1.25fr)
				'owner  parcel' 1fr;
		}
		/* .wrapper {
			flex-direction: row;
		}
		.owner-section {
			flex-direction: column;
		}
		.owner-label {
			bottom: auto;
			left: auto;
			top: 1rem;
			right: 1rem;
		}
		.parcel-label {
			bottom: auto;
			left: 1rem;
			top: 1rem;
			right: auto;
		} */
	}

	.owner-cell {
		grid-area: owner;
	}
	.parcel-cell {
		grid-area: parcel;
	}
	.legend {
		grid-area: legend;
	}

	.cell {
		position: relative;
		container-type: size;
		display: grid;
		place-items: center;
		min-width: 0;
		min-height: 0;
	}

	.frame {
		position: relative;
	}

	.owner-frame {
		aspect-ratio: var(--ratio-owner);
		width: min(100cqw, 100cqh * var(--ratio-owner));
	}

	.parcel-frame {
		aspect-ratio: var(--ratio-parcel);
		width: min(100cqw, 100cqh * var(--ratio-parcel));
		background-color: #ece9e8;
	}

	.owner-section {
		position: relative;
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 0 0.75rem;
		/* gap: 2rem; */
	}

	.owner-map {
		position: relative;
		/* flex: 0 0 auto; */
		/* margin: 0 auto; */
		/* top: 20px;
        right: 20px; */
		width: clamp(350px, 50vw, 600px);
		/* height: clamp(280px, 30dvh, 600px); */
		aspect-ratio: 3554/2400;
		/* padding: 0 2rem; */
		/* z-index: 2; */
		/* border-radius: 8px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        background: white;
		border: 0.25px solid grey; */
	}

	.caption-box {
		position: relative;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		gap: 0px 5px;
		/* flex: 0 0 auto; */
		/* top: 20px;
		left: 20px; */
		/* width: clamp(240px, 30vw, 450px); */
		/* z-index: 3; */
		/* text-align: center; */
		/* border: 0.25px solid grey; */
	}

	.legend {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		align-content: center;
		gap: 0.2rem 0.85rem;
		min-height: 0;
	}

	.lede {
		flex: 0 0 100%;
		margin: 0 0 0.25rem;
		text-align: center;
		opacity: 0;
	}

	.caption {
		font-family: 'Host Grotesk', sans-serif;
		font-size: clamp(0.8rem, 1.6vh, 1rem);
		font-weight: 500;
		line-height: 1.3;
		opacity: 0;
	}

	.parcel-map {
		flex: 1;
		position: relative;
		background-color: #ece9e8;
	}

	.layer {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: contain;
		opacity: 0;
		border: 1px solid green;
	}

	.map-label {
		position: absolute;
		top: 0.5rem;
		right: 0.5rem;
		margin: 0;
		font-size: clamp(0.7rem, 1.4vh, 0.85rem);
		z-index: 1;
	}

	.owner-label {
		position: absolute;
		font-size: 0.8rem;
		bottom: 0.5rem;
		right: 0.5rem;
	}

	.parcel-label {
		position: absolute;
		font-size: 0.8rem;
		top: 0.5rem;
		right: 0.5rem;
	}
</style>
