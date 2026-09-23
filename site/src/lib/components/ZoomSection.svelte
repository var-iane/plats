<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper;
	let examples;
	let introParts = $state([]);

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

		// tl.from(introParts, { opacity: 0, y: 20, duration: 1, stagger: 2 }, 0);

		tl.from(examples, { opacity: 0, duration: 1 }, 6)

		return () => {
			tl.scrollTrigger?.kill();
			tl.kill();
		};
	});
</script>

<div class="wrapper">
	<div class="intro-pin" bind:this={pinnedWrapper}>
		<div class="intro">
			<h2>Artificial enclaves</h2>
			<p bind:this={introParts[0]}>
				Sales reps were given a limited batch of inventory to sell at a time — say, certain blocks
				within a specific unit of a subdivision. Horizon had sales offices across the U.S. and
				abroad, so a rep's territory influenced which customers could buy where.
			</p>
			<p bind:this={introParts[1]}>
				At sales dinner parties, reps were known to open envelopes ("and here are tonight's lots!") and warn attendees that these choice parcels could be gone by morning.
			</p>
			<p bind:this={introParts[2]}>
				This is the likeliest explanation for what's visible in the ownership data: pockets of
				buyers from the same place, a mini-Minneapolis in one unit, a New New York in the next.
			</p>
		</div>
	</div>

	<!-- <div class="examples">
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
					<p class="chip">
						<span style="color: #2f8ac4; font-weight: 500;">Cleveland:</span> Lots 8-14
					</p>
					<p class="chip">
						<span style="color: #ff6b5a; font-weight: 500;">North Rhine-Westphalia, Germany:</span> Lots
						3, 6, 15, 17, 34
					</p>
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
					<div class="key-row">
						<span style="color: #3a3b78; font-weight: 500;">Las Vegas:</span> Lots 4, 7
					</div>
					<div class="key-row">
						<span style="color: #1ebecf; font-weight: 500;">British Columbia, Canada:</span> Lots 5, 6
					</div>
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
					<p class="chip">
						<span style="color: #d326be; font-weight: 500;">Birmingham:</span> Lot 55
					</p>
					<p class="chip">
						<span style="color: #9966cc; font-weight: 500;">Portland:</span> Lot 59
					</p>
					<p class="chip"><span style="color: #e73f74; font-weight: 500;">Chicago:</span> Lot 73</p>
					<p class="chip"><span style="color: #94a800; font-weight: 500;">Phoenix:</span> Lot 68</p>
					<p class="chip">
						<span style="color: #ffa600; font-weight: 500;">New York City:</span> Lots 27-33
					</p>
				</div>
			</div>
		</figure>
	</div> -->

	<div class="examples" bind:this={examples}>
		<figure class="example">
			<div class="example-header">
				<h3>Shadow Ridge subdivision</h3>
				<img
					class="locator"
					src={`${base}/images/zooms/shadow-ridge.png`}
					alt="Location of Shadow Ridge subdivision"
				/>
			</div>

			<div class="stage">
				<div class="stage-map">
					<img
						class="zoom shadow-ridge-zoom"
						src={`${base}/images/zooms/subdivision-enclaves_shadow-ridge.png`}
						alt="Parcels in Shadow Ridge colored by owner residence"
					/>
				</div>
				<ul class="key">
					<li><span class="dot" style="background:#2f8ac4"></span><strong>Cleveland</strong> <em>Lots 8-14</em></li>
					<li>
						<span class="dot" style="background:#ff6b5a"></span><strong>North Rhine-Westphalia, Germany</strong>
						<em>Lots 3, 6, 15, 17, 34</em>
					</li>
				</ul>
			</div>
		</figure>

		<figure class="example">
			<div class="example-header">
				<h3>Mountain Vista subdivision</h3>
				<img
					class="locator"
					src={`${base}/images/zooms/mountain-vista.png`}
					alt="Location of Mountain Vista subdivision"
				/>
			</div>
			<div class="stage">
				<div class="stage-map">
					<img
						class="zoom mountain-vista-zoom"
						src={`${base}/images/zooms/subdivision-enclaves_mountain-vista.png`}
						alt="Parcels in Mountain Vista colored by owner residence"
					/>
				</div>
				<ul class="key">
					<li><span class="dot" style="background: #3a3b78"></span><strong>Las Vegas</strong><em>Lots 4, 7</em></li>
					<li>
						<span class="dot" style="background: #1ebecf"></span><strong>British Columbia, Canada</strong><em
							>Lots 5, 6</em
						>
					</li>
				</ul>
			</div>
		</figure>

		<figure class="example">
			<div class="example-header">
				<h3>Horizon City Estates subdivision</h3>
				<img
					class="locator"
					src={`${base}/images/zooms/horizon-city-estates.png`}
					alt="Location of Horizon City Estates subdivision"
				/>
			</div>
			<div class="stage">
				<div class="stage-map">
					<img
						class="zoom horizon-city-estates-zoom"
						src={`${base}/images/zooms/subdivision-enclaves_horizon-city-estates.png`}
						alt="Parcels in Horizon City Estates colored by owner residence"
					/>
				</div>
				<ul class="key">
					<li><span class="dot" style="background: #d326be"></span><strong>Birmingham</strong><em>Lot 55</em></li>
					<li><span class="dot" style="background: #9966cc"></span><strong>Portland</strong><em>Lot 59</em></li>
					<li><span class="dot" style="background: #e73f74"></span><strong>Chicago</strong><em>Lot 73</em></li>
					<li><span class="dot" style="background: #94a800"></span><strong>Phoenix</strong><em>Lot 68</em></li>
					<li><span class="dot" style="background: #ffa600"></span><strong>New York City</strong><em>Lots 27-33</em></li>
				</ul>
			</div>
		</figure>
	</div>
</div>

<style>
	.wrapper {
		/* display: flex;
		flex-direction: column;
		align-items: center; */
		background-color: #ece9e8;
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
		margin: 0 0 1rem 0;
		/* padding: 6px 0; */
	}

	h3 {
		font-family: 'Epilogue', sans-serif;
		font-weight: 600;
		/* margin: 0 0 1rem 0; */
		/* padding: 6px 0; */
	}

	.intro p {
		font-family: 'Host Grotesk', 'Epilogue', sans-serif;
		font-weight: 300;
		margin: 0 0 1rem 0;
	}

	.intro-pin {
		/* min-height: 100svh; */
		display: flex;
		/* align-items: center; */
		justify-content: center;
		padding: 3rem 1rem;
	}

	.intro {
		max-width: 42rem;
	}

	.examples {
		--scale: 0.613; /* to make widest image fit max column width */

		max-width: 63rem;
		margin: 0 auto;
		padding: 3rem 1rem;
	}

	.example {
		/* display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 1rem 0.2rem;
		padding: 20px 0; */
		/* display: flex;
		gap: 1rem;
		align-items: flex-start;
		flex-wrap: wrap; */
		/* margin: 0 0 3.5rem 0; */
		padding: 2rem 0;
		border-top: 1px solid rgba(0, 0, 0, 0.3);
	}

	.example-header {
		display: flex;
		align-items: center;
		gap: 1.5rem;
		margin-bottom: 1rem;
		
	}

	.shadow-ridge-zoom {
		width: calc(495px * var(--scale));
	}
	.mountain-vista-zoom {
		width: calc(173px * var(--scale));
	}
	.horizon-city-estates-zoom {
		width: calc(1094px * var(--scale));
		max-width: min(100%, 520px);
	}

	.locator {
		/* display: block;
		width: 100%;
		max-width: 450px;
		border: 1px solid black;
		margin-bottom: 1.5rem; */
		width: 100px;
		flex-shrink: 0;
		/* border: 1px solid black; */
		display: block;
	}

	.stage {
		display: flex;
		align-items: flex-start;
		gap: 2rem;
		flex-wrap: wrap;
		min-height: 0px;
		max-width: 100%;
		/* padding: 1rem 2rem; */
		/* background: #ece9e8; */
		/* border: 1px solid black; */
	}

	.stage-map {
		flex: 0 1 auto;
		display: flex;
		align-items: center;
		justify-content: center;
		min-width: 200px;
	}

	.zoom {
		display: block;
		max-width: 100%;
		/* border: 1px solid black; */
	}

	.key {
		flex: 0 1 auto;
		max-width: 320px;
		min-width: 0;
		list-style: none;
		margin: 0;
		padding: 0;
		font-family: 'Host Grotesk', sans-serif;
		font-size: 0.85rem;
		/* font-weight: 300; */
		line-height: 1.2;
	}

	.key li {
		display: flex;
		align-items: baseline;
		gap: 0.45rem;
		padding: 0.3rem 0;
		border-bottom: 1px solid rgba(0, 0, 0, 0.08);
	}

	.key li:last-child {
		border-bottom: none;
	}

	.key strong {
		/* font-weight: 400; */
		/* max-width: 220px; */
	}

	.key em {
		margin-left: auto;
		font-style: normal;
		font-weight: 300;
		opacity: 0.6;
		white-space: nowrap;
	}

	.dot {
		width: 0.5rem;
		height: 0.5rem;
		border-radius: 2px;
		flex-shrink: 0;
		align-self: center;
	}

	/* .key span {
		font-weight: 500;
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

	/* @media (max-width: 720px) {
		.examples {
			--scale: 0.45;
		}
	} */

	@media (max-width: 720px) {
		.stage {
			flex-direction: column;
			align-items: flex-start;
			/* min-height: 0; */
		}
		.example-header {
			flex-direction: column;
			align-items: flex-start;
			gap: 0.75rem;
		}
	}
</style>
