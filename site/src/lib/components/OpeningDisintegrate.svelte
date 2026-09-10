<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	gsap.registerPlugin(ScrollTrigger);

	// disintegration effect: put an image into the canvas element, chop it into 75 pixel buckets, copy those buckets into output canvases in the same positions, then animate each bucket (collection of pixels) flying off and fading in a staggered order
    // adapted from this: https://codepen.io/dev_loop/pen/mdVWRMv

	let baseCanvas;
	let wrapper;

	const COUNT = 75;
	const REPEAT_COUNT = 3;

	onMount(() => {
		const img = new Image(); // this creates a new img element to put my image into
		img.src = '/phantom-plats/images/opening/vintagemap2.png';

		img.onload = () => {
			const width = img.width;
			const height = img.height;

			baseCanvas.width = 800;
			baseCanvas.height = 600;
            // baseCanvas.width = width;
			// baseCanvas.height = height;
			const ctx = baseCanvas.getContext('2d');
			ctx.drawImage(img, 0, 0);

			const imageData = ctx.getImageData(0, 0, width, height); //
			let dataList = [];
            

			for (let i = 0; i < COUNT; i++) {
				dataList.push(ctx.createImageData(width, height));
			}

			// determine which bucket (output canvas) each pixel belongs to - for every (x,y) compute a dataIndex. the math biases the choice by a mix of left horizontal position (x) and randomness, so left-side pixels are more likely to belong to low-numbered shards (giving a sort of left-to-right disintegration effect)
			for (let x = 0; x < width; x++) {
				for (let y = 0; y < height; y++) {
					for (let l = 0; l < REPEAT_COUNT; l++) {
						const index = (x + y * width) * 4;
						const dataIndex = Math.floor((COUNT * (Math.random() + (2 * x) / width)) / 3);
						for (let p = 0; p < 4; p++) {
							dataList[dataIndex].data[index + p] = imageData.data[index + p];
						}
					}
				}
			}

			// hide the original canvas
			// baseCanvas.style.display = 'none';

			// create a new canvas element for each pixel bucket, draw the bucket's pixels onto it in the same position, and append to the page. the "cloned-canvas" CSS class positions all canvases in the same position, so all of the output canvases are stacked on top of each other, making up what looks like the original image
			dataList.forEach((data, i) => {
				let clonedCanvas = baseCanvas.cloneNode(); // clones attributes like width, height but not drawn content
				clonedCanvas.getContext('2d').putImageData(data, 0, 0);
				clonedCanvas.className = 'cloned-canvas';
				wrapper.appendChild(clonedCanvas);

                // animation
				const randomAngle = (Math.random() - 0.5) * 2 * Math.PI;  // random direction
				const randomRotationAngle = 30 * (Math.random() - 0.5);  // random rotation

				let tl = gsap.timeline({
					scrollTrigger: {
						trigger: wrapper,
                        // pin: true,
						scrub: 1,
                        markers: true,
						start: 'top top',
						end: () => window.innerHeight * 2
					}
				});

				tl.to(clonedCanvas, {
					duration: 1,
					rotate: randomRotationAngle,
					translateX: 40 * Math.sin(randomAngle),
					translateY: 40 * Math.cos(randomAngle),
					opacity: 0,
					delay: (i / dataList.length) * 2
				});
			});
		};
	});
</script>

<div class="wrapper" bind:this={wrapper}>
	<canvas bind:this={baseCanvas}></canvas>
	<!-- <h1>Phantom Plats</h1> -->
</div>

<style>
	.wrapper {
		position: fixed;
		height: 100vh;
		width: 100%;
        justify-content: safe center;
        align-items: center;
		background-color: sandybrown;
		overflow: hidden;
	}

	canvas {
		border: 1px solid black;
        position: fixed;
	}

    /* don't add the scoped class name */
	:global(.cloned-canvas) {
		position: fixed;
		top: 0;
		left: 0;
	}
</style>
