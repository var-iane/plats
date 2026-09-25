<script>
	import { base } from '$app/paths';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);
	ScrollTrigger.config({ ignoreMobileResize: true });

	let pinnedWrapper, intro, examples;

	onMount(() => {
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: pinnedWrapper,
				start: 'top top',
				end: () => '+=' + Math.min(Math.max(window.innerHeight * 1.2, 700), 1200),
				pin: true,
				scrub: 1,
				anticipatePin: 1,
				invalidateOnRefresh: true
			}
		});

		tl.from([intro, examples], { opacity: 0, duration: 2 }, 0).to({}, { duration: 10 });

		window.addEventListener('load', () => ScrollTrigger.refresh());

		return () => {
			tl.scrollTrigger?.kill();
			tl.kill();
		};
	});
</script>

<div class="wrapper" bind:this={pinnedWrapper}>
	<div class="intro" bind:this={intro}>
		<h2>Artificial enclaves</h2>
		<p>
			Why were buyers in different places sold different inventory?
		</p>
		<p>
			Sales reps were given a limited batch of lots to sell at a time — say, certain blocks
			within a specific unit of a subdivision. Horizon had sales offices across the U.S. and abroad,
			so a rep's territory influenced which customers could buy where.
		</p>
		<p>
			At sales dinner parties, reps were known to open envelopes ("and here are tonight's lots!")
			and warn attendees that these choice parcels could be gone by morning.
		</p>
		<p>
			This is the likeliest explanation for what's visible in the ownership data: pockets of buyers
			from the same place, a mini-Minneapolis in one unit, a New New York in the next.
		</p>
	</div>

	<div class="examples" bind:this={examples}>
		<figure class="example">
			<div class="example-header">
				<img
					class="locator"
					src={`${base}/images/zooms/shadow-ridge.png`}
					alt="Location of Shadow Ridge subdivision"
				/>
				<h3>Shadow Ridge<br />subdivision</h3>
			</div>

			<div class="map">
				<img
					class="zoom shadow-ridge-zoom"
					src={`${base}/images/zooms/subdivision-enclaves_shadow-ridge.png`}
					alt="Parcels in Shadow Ridge colored by owner residence"
				/>
			</div>
			<ul class="key">
				<li>
					<span class="dot" style="background:#2f8ac4"></span><strong>Cleveland</strong>
					<em>Units 8-14</em>
				</li>
				<li>
					<span class="dot" style="background:#ff6b5a"></span><strong
						>North Rhine-Westphalia, Germany</strong
					>
					<em>Units 3, 6, 15, 17, 34</em>
				</li>
			</ul>
			
		</figure>

		<figure class="example">
			<div class="example-header">
				<img
					class="locator"
					src={`${base}/images/zooms/mountain-vista.png`}
					alt="Location of Mountain Vista subdivision"
				/>
				<h3>Mountain Vista<br />subdivision</h3>
			</div>
				<div class="map">
					<img
						class="zoom mountain-vista-zoom"
						src={`${base}/images/zooms/subdivision-enclaves_mountain-vista.png`}
						alt="Parcels in Mountain Vista colored by owner residence"
					/>
				</div>
				<ul class="key">
					<li>
						<span class="dot" style="background: #3a3b78"></span><strong>Las Vegas</strong><em
							>Units 4, 7</em
						>
					</li>
					<li>
						<span class="dot" style="background: #1ebecf"></span><strong
							>British Columbia, Canada</strong
						><em>Units 5, 6</em>
					</li>
				</ul>
		</figure>

		<figure class="example">
			<div class="example-header">
				<img
					class="locator"
					src={`${base}/images/zooms/horizon-city-estates.png`}
					alt="Location of Horizon City Estates subdivision"
				/>
				<h3>Horizon City Estates<br />subdivision</h3>
			</div>

				<div class="map">
					<img
						class="zoom horizon-city-estates-zoom"
						src={`${base}/images/zooms/subdivision-enclaves_horizon-city-estates.png`}
						alt="Parcels in Horizon City Estates colored by owner residence"
					/>
				</div>
				<ul class="key">
					<li>
						<span class="dot" style="background: #d326be"></span><strong>Birmingham</strong><em
							>Unit 55</em
						>
					</li>
					<li>
						<span class="dot" style="background: #9966cc"></span><strong>Portland</strong><em
							>Unit 59</em
						>
					</li>
					<li>
						<span class="dot" style="background: #e73f74"></span><strong>Chicago</strong><em
							>Unit 73</em
						>
					</li>
					<li>
						<span class="dot" style="background: #94a800"></span><strong>Phoenix</strong><em
							>Unit 68</em
						>
					</li>
					<li>
						<span class="dot" style="background: #ffa600"></span><strong>New York City</strong><em
							>Units 27-33</em
						>
					</li>
				</ul>
		</figure>
	</div>
</div>

<style>
	.wrapper {
		background-color: #ece9e8;
		padding: 0 1rem;
	}

	h2 {
		font-family: 'Epilogue', sans-serif;
		margin: 0 0 1rem 0;
		/* padding: 6px 0; */
	}

	h3 {
		font-family: 'Epilogue', sans-serif;
		font-weight: 500;
		/* margin: 0 0 1rem 0; */
		/* padding: 6px 0; */
	}

	.intro p {
		font-family: 'Host Grotesk', 'Epilogue', sans-serif;
		font-weight: 300;
		margin: 0 0 1rem 0;
	}

	.intro,
	.examples {
		max-width: 42rem;
		margin: 0 auto;
	}

	.intro {
		padding: 3rem 0 0 0;
	}

	.examples {
		--scale: 0.613;
		--map-col: 350px;
		padding: 3rem 0rem;
	}

	.example {
		display: grid;
		grid-template-columns: var(--map-col) 1fr;
		grid-template-areas:
			'header header'
			'map    key';
		gap: 2.5rem 2rem;
		padding: 2.5rem 0;
		margin: 0;
		border-top: 1px solid rgba(0, 0, 0, 0.12);
	}

	.example-header {
		grid-area: header;
		display: flex;
		align-items: center;
		gap: 1.25rem;
		/* margin-bottom: 1rem; */
	}

	.locator {
		display: block;
		width: 100px;
		flex-shrink: 0;
		/* border: 1px solid black; */
	}

	.map {
		grid-area: map;
		display: flex;
		align-items: flex-start;
		justify-content: center;
	}

	.zoom {
		display: block;
		max-width: 100%;
		height: auto;
		/* border: 1px solid black; */
	}

	.shadow-ridge-zoom {
		width: calc(495px * var(--scale));
	}
	.mountain-vista-zoom {
		width: calc(173px * var(--scale));
	}
	.horizon-city-estates-zoom {
		width: calc(1094px * var(--scale));
	}

	.key {
		grid-area: key;
		align-self: start;
		list-style: none;
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
		text-wrap: balance;
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

	@media (max-width: 640px) {
		.example {
			grid-template-columns: 1fr;
			grid-template-areas:
				'header'
				'map'
				'key';
			gap: 0.5rem;
		}
		.map {
			justify-content: flex-start;
		}
		.example-header {
			/* flex-direction: column; */
			align-items: flex-start;
			gap: 0.75rem;
		}
	}
</style>
