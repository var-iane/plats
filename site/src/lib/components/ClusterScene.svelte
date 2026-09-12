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
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7, cap8, cap9, cap10, cap11, cap12;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=3000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
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
			.to(otherParcels, { opacity: 1, duration: 0.25 }, '>');

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
	<div class="owner-section">
		<p class="owner-label">Where owners lived</p>

		<div class="caption-box">
			<p bind:this={cap1} class="caption">People bought in from...</p>
			<p bind:this={cap2} style="color: #ffa100" class="caption">New York City</p>
			<p bind:this={cap3} style="color: #ffa100" class="caption">Chicago</p>
			<p bind:this={cap4} style="color: #ffa100" class="caption">Cleveland</p>
			<p bind:this={cap5} style="color: #ffa100" class="caption">Seattle</p>
			<p bind:this={cap6} style="color: #ffa100" class="caption">Portland</p>
			<p bind:this={cap7} style="color: #ffa100" class="caption">Phoenix</p>
			<p bind:this={cap8} style="color: #ffa100" class="caption">Minneapolis</p>
			<p bind:this={cap9} style="color: #ffa100" class="caption">Birmingham</p>
			<p bind:this={cap10} style="color: #ffa100" class="caption">St. Louis</p>
			<p bind:this={cap11} style="color: #ffa100" class="caption">Las Vegas</p>
			<p bind:this={cap12} style="color: #ffa100" class="caption">and all around</p>
		</div>

		<div class="owner-map">
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
			<img
				bind:this={other}
				src={`${base}/images/owner-clusters/10-clusters.svg`}
				alt=""
				class="layer"
			/>
		</div>
	</div>

	<div class="parcel-map">
		<p class="parcel-label">Where they bought parcels</p>
		<img
			bind:this={units}
			src={`${base}/images/parcel-clusters/units-filled-white.svg`}
			alt=""
			style="fill: white"
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
			src={`${base}/images/parcel-clusters/10-clusters.svg`}
			alt=""
			class="layer"
		/>
	</div>
</div>

<style>
	.wrapper {
		position: relative;
		width: 100%;
		height: 100vh;
		height: 100lvh;
		display: flex;
		flex-direction: column;
		overflow: hidden;
	}

	.owner-section {
		position: relative;
		display: flex;
		flex: 1;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding: 0 0.75rem;
		gap: 2rem;
	}

	.owner-map {
		position: relative;
		/* flex: 0 0 auto; */
		/* margin: 0 auto; */
		/* top: 20px;
        right: 20px; */
		width: clamp(280px, 50vw, 600px);
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
		/* flex: 0 0 auto; */
		/* top: 20px;
		left: 20px; */
		/* width: clamp(240px, 30vw, 450px); */
		/* z-index: 3; */
		/* text-align: center; */
		/* border: 0.25px solid grey; */
		font-family: "Host Grotesk", sans-serif;
		font-size: 1rem;
		font-weight: 300;
		line-height: 1.3;
	}

	.caption {
		/* font-family: "Host Grotesk", sans-serif;
		font-size: 1rem;
		font-weight: 300;
		line-height: 1.3; */
		opacity: 0;
	}

	.parcel-map {
		flex: 2;
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

	@media (min-aspect-ratio: 1/1) {
		.wrapper {
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
		}
	}
</style>
