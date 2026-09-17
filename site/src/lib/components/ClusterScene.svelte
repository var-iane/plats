<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	const cities = [
		{ id: 'nyc', name: 'New York City', color: '#ffa100', x: 94.0, y: 33.1, anchor: 'right' },
		{ id: 'chicago', name: 'Chicago', color: '#e73f74', x: 68.9, y: 35.2, anchor: 'right' },
		{ id: 'cleveland', name: 'Cleveland', color: '#2f8ac4', x: 70.8, y: 42.4, anchor: 'left' },
		{ id: 'seattle', name: 'Seattle', color: '#11a579', x: 11.0, y: 11.7, anchor: 'left' },
		{ id: 'portland', name: 'Portland', color: '#9966cc', x: 6.3, y: 21.4, anchor: 'left' },
		{ id: 'phoenix', name: 'Phoenix', color: '#94a800', x: 17.1, y: 61.8, anchor: 'left' },
		{ id: 'minneapolis', name: 'Minneapolis', color: '#6666cc', x: 50.0, y: 26.0, anchor: 'left' },
		{ id: 'birmingham', name: 'Birmingham', color: '#d326be', x: 66.4, y: 64.5, anchor: 'left' },
		{ id: 'stlouis', name: 'St. Louis', color: '#1ebecf', x: 58.8, y: 47.0, anchor: 'left' },
		{ id: 'lasvegas', name: 'Las Vegas', color: '#3a3b78', x: 13.7, y: 51.3, anchor: 'left' }
		// { id: 'international', name: 'military stationed overseas', color: '#ff6b5a', x: 4.0, y: 81.5, anchor: 'left' },
	];

	let pinnedWrapper, ownerFrame, parcelCell;
	let usMap, horizonLabel, horizonDot, ownerNote, distances, units;
	let subhead1, subhead2;
	let other, otherParcels, internationalNote, internationalParcels;
	let cap1, cap2, cap3, cap4, cap5, cap6, cap7, cap8, cap9, cap10, cap11, cap12, cap13;

	let ownerLayers = $state([]);
	let parcelLayers = $state([]);
	let labels = $state([]);
	let headlines = $state([]);

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: '+=8000',
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				invalidateOnRefresh: true
			}
		});

		if (import.meta.env.DEV) {
			ownerFrame.addEventListener('click', (e) => {
				const r = ownerFrame.getBoundingClientRect();
				console.log(
					`x: ${(((e.clientX - r.left) / r.width) * 100).toFixed(1)}, y: ${(((e.clientY - r.top) / r.height) * 100).toFixed(1)}`
				);
			});
		}

		const BEAT = 6;
		const DIM = 0.15;

		// initial states
		gsap.set([ownerNote, parcelCell], { opacity: 0 });

		// beat 1: owner map + distance-band points
		tl.to([subhead1, usMap, horizonLabel, horizonDot], { opacity: 1, duration: 3 }, 0)
			.to([ownerNote, distances], { opacity: 1, duration: 3 }, 6)
			.to({}, { duration: 20 });

		// beat 2: transition
		tl.addLabel('transition', 20)
			.to(
				[horizonLabel, horizonDot, distances, subhead1],
				{ opacity: 0, duration: 3 },
				'transition'
			)
			.to([subhead2, parcelCell, units], { opacity: 1, duration: 3 }, 'transition+=1')
			.to({}, { duration: 5 });

		// beat 3: city clusters
		tl.addLabel('citiesStart', 'transition+=10');

		cities.forEach((city, i) => {
			const at = `city${i}`;
			tl.addLabel(at, i === 0 ? 'citiesStart' : `city${i - 1}+=${BEAT}`);

			tl.to(
				[labels[i], headlines[i], ownerLayers[i], parcelLayers[i]],
				{ opacity: 1, duration: 2 },
				at
			);

			if (i > 0) {
				tl.to(
					[labels[i - 1], ownerLayers[i - 1], parcelLayers[i - 1]],
					{ opacity: DIM, duration: 2 },
					at
				).to(headlines[i - 1], { opacity: 0, duration: 2 }, at);
			}
		});

		tl.addLabel('allOn', `city${cities.length - 1}+=${BEAT}`)
			.to(
				[...labels, ...headlines, ...ownerLayers, ...parcelLayers],
				{ opacity: 1, duration: 3 },
				'allOn'
			)
			.to({}, { duration: 6 })

			.addLabel('international', 'allOn+=9')
			.to([usMap, other, ...labels, ...ownerLayers, ...parcelLayers], { opacity: 0, duration: 3 }, 'international')
			.to(internationalParcels, { opacity: 1, duration: 2 }, 'international+=2')
			.to(internationalNote, { opacity: 1, duration: 2 }, `international+=2`)
			.to({}, { duration: 10 });

		return () => {
			tl.scrollTrigger?.kill();
			tl.kill();
		};
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="subhead-box">
		<p class="subhead" bind:this={subhead1}>
			80% of buyers lived <span style="color: #ca6e56">at least 500 miles away</span>.
		</p>
		<p class="subhead" bind:this={subhead2}>
			Buyers in different places were sold different inventory.
		</p>
	</div>

	<div class="cell owner-cell">
		<p class="map-label map-label-owner" bind:this={ownerNote}>Where buyers lived</p>
		<div class="frame owner-frame" bind:this={ownerFrame}>
			<img
				src={`${base}/images/owner-clusters/basemap.svg`}
				alt=""
				class="layer"
				bind:this={usMap}
			/>

			<span class="city-dot" style="left: 30.7%; top: 73.3%;" bind:this={horizonDot}></span>

			<span class="city-label" style="left: 22.1%; top: 77.3%" bind:this={horizonLabel}
				>Horizon City</span
			>

			<img
				src={`${base}/images/owner-clusters/distances.png`}
				alt=""
				class="layer"
				bind:this={distances}
			/>

			{#each cities as city, i (city.id)}
				<img
					src={`${base}/images/owner-clusters/${city.id}.svg`}
					alt=""
					class="layer"
					bind:this={ownerLayers[i]}
				/>
			{/each}

			<!-- <img src={`${base}/images/owner-clusters/other.png`} alt="" class="layer" bind:this={other} /> -->

			{#each cities as city, i (city.id)}
				<span
					class="city-label"
					class:anchor-right={city.anchor === 'right'}
					style="left: {city.x}%; top: {city.y}%; color: {city.color}"
					bind:this={labels[i]}>{city.name}</span
				>
			{/each}

			<p class="international-note" bind:this={internationalNote}>
				<span style="color: #ff6b5a; font-weight: 600;">All around the world</span>: military
				members stationed overseas, residents of Guam, Germany, Japan.
			</p>
		</div>
	</div>

	<!-- <p class="city-headline">
		{#each cities as city, i (city.id)}
			<span style="color: {city.color}" bind:this={headlines[i]}>{city.name}</span>
		{/each}
	</p> -->

	<div class="cell parcel-cell" bind:this={parcelCell}>
		<p class="map-label map-label-parcel">Where they bought parcels</p>

		<div class="frame parcel-frame">
			<img
				bind:this={units}
				src={`${base}/images/parcel-clusters/units-filled-white.svg`}
				alt=""
				class="layer"
			/>

			{#each cities as city, i (city.id)}
				<img
					src={`${base}/images/parcel-clusters/${city.id}.svg`}
					alt=""
					class="layer"
					bind:this={parcelLayers[i]}
				/>
			{/each}

			<!-- <img
				src={`${base}/images/parcel-clusters/other.png`}
				alt=""
				class="layer"
				bind:this={otherParcels}
			/> -->

			<img
				src={`${base}/images/parcel-clusters/international.svg`}
				alt=""
				class="layer"
				bind:this={internationalParcels}
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
		height: 100dvh;
		overflow: hidden;
		box-sizing: border-box;
		/* padding: clamp(0.5rem, 2vh, 1.25rem); */
		/* gap: clamp(0.5rem, 2vh, 1.25rem); */
		font-family: 'Epilogue', sans-serif;
		display: grid;
		align-content: center;
		grid-template:
			'subhead' auto
			'owner' 1fr
			'parcel' 1fr / minmax(0, 1fr);
	}

	.cell {
		position: relative;
		container-type: size;
		display: grid;
		place-items: center;
		min-width: 0;
		min-height: 0;
		/* border: 1px solid red; */
	}

	.owner-cell {
		grid-area: owner;
	}
	.parcel-cell {
		grid-area: parcel;
		background-color: #ece9e8;
	}

	.frame {
		position: relative;
		container-type: inline-size;
		/* border: 1px solid green; */
	}

	.owner-frame {
		aspect-ratio: var(--ratio-owner);
		width: min(100cqw, 100cqh * var(--ratio-owner));
	}

	.parcel-frame {
		aspect-ratio: var(--ratio-parcel);
		width: min(100cqw, 100cqh * var(--ratio-parcel));
		/* background-color: #ece9e8; */
	}

	.subhead-box {
		grid-area: subhead;
		position: relative;
		min-height: 3rem;
		margin: 1rem 0;
	}

	.subhead {
		position: absolute;
		/* top: 50%; */
		/* left: 50%;
		transform: translate(-50%, -50%); */
		inset: 0;
		/* padding: 2rem 0; */
		font-size: clamp(1rem, 2vh, 1.5rem);
		font-weight: 300;
		line-height: 1.35;
		text-align: center;
		text-wrap: balance;
		opacity: 0;
	}

	.international-note {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 65cqw;
		font-family: 'Host Grotesk', sans-serif;
		font-size: clamp(0.9rem, 2cqw, 1.5rem);
		font-weight: 300;
		line-height: 1.4;
		text-align: center;
		text-wrap: balance;
		opacity: 0;
		z-index: 3;
	}

	.city-label {
		position: absolute;
		transform: translate(0.5em, -50%);
		font-family: 'Host Grotesk', sans-serif;
		font-size: clamp(0.75rem, 2cqw, 1.5rem);
		font-weight: 500;
		white-space: nowrap;
		opacity: 0;
		z-index: 2;
		paint-order: stroke fill;
		-webkit-text-stroke: 3px rgba(255, 255, 255, 0.85);
	}
	.city-label.anchor-right {
		transform: translate(calc(-100% - 0.5em), -50%);
	}

	.city-dot {
		position: absolute;
		width: 2px;
		height: 7px;
		/* border-radius: 50%; */
		background: #1a1a1a;
		transform: translate(-50%, -50%);
		opacity: 0;
		z-index: 3;
		box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.9);
	}

	
	/* .city-headline {
		display: none;
	} */

	.layer {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: contain;
		opacity: 0;
		/* border: 1px solid green; */
	}

	.map-label {
		position: absolute;
		top: 0.5rem;
		right: 0.5rem;
		font-weight: 300;
		font-style: italic;
		font-size: clamp(0.7rem, 1.4vh, 0.85rem);
		z-index: 3;
	}

	@media (min-aspect-ratio: 1/1) {
		.wrapper {
			grid-template:
				'subhead subhead' auto
				'owner  parcel' 1fr / minmax(0, 1.4808fr) minmax(0, 1.25fr);
		}
		.map-label-owner {
			position: absolute;
			top: 1rem;
			right: 1rem;
			font-size: clamp(0.7rem, 1.4vh, 0.85rem);
			z-index: 3;
		}
		.map-label-parcel {
			position: absolute;
			top: 1rem;
			left: 1rem;
			font-size: clamp(0.7rem, 1.4vh, 0.85rem);
			z-index: 3;
		}
	}

	@media (max-width: 520px) {
		.wrapper {
			grid-template:
				'subhead' auto
				/* 'headline' auto */
				'owner' 1fr
				'parcel' 1fr / minmax(0, 1fr);
		}
		.map-label {
			position: absolute;
			top: 0.5rem;
			left: 0.5rem;
			font-size: clamp(0.7rem, 1.4vh, 0.85rem);
			z-index: 3;
		}
		/* .city-label { display: none; } */
		/* .city-headline {
			grid-area: headline;
			position: relative;
			display: block;
			margin: 0;
			height: 1.6em;
			font-family: 'Host Grotesk', sans-serif;
			font-size: 1.15rem;
			font-weight: 600;
			line-height: 1.6;
			text-align: center;
		}
		.city-headline span {
			position: absolute;
			inset: 0;
			opacity: 0;
			white-space: nowrap;
		} */
	}

	@media (prefers-reduced-motion: reduce) {
		.layer,
		.city-label {
			opacity: 1;
		}
	}
</style>
