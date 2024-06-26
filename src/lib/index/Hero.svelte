<script>
	import Loading from './Loading.svelte';
	import DiscButton from '$lib/buttons/disc-button.svelte';
	import RingButton from '$lib/buttons/ring-button.svelte';

	import { draw, fade } from 'svelte/transition';

	import SectionHeader from '$lib/SectionHeader.svelte';
	import BGLogo from '$lib/background/BGLogo.svelte';
	import Arrow from '$lib/Arrow.svelte';
import { onMount } from 'svelte';

	let pageLoaded = false;

	onMount(() => {
		pageLoaded = true;
	})

	$: {
		setTimeout(() => {
		}, 1000);
	}

	let circleHeight;
	let svgEl;

	// Detect Firefox
	var isFirefox = typeof InstallTrigger !== 'undefined';

	$: {
		if (svgEl !== undefined) {
			setTimeout(() => {
				const cutoutHeight = svgEl.height.animVal.value;
				circleHeight = cutoutHeight * `${isFirefox ? 0.3 : 0.42}`;
			}, 100);
		}
	}

	const scrollToServices = () => {
		let deviceHeight = document.documentElement.clientHeight;
		window.scrollTo(0, deviceHeight);
	};
</script>

<section class="hero" in:fade={{ duration: 1000 }}>
	<video
		class="hero-vid"
		autoplay
		playsinline
		muted
		loop
		in:fade
		src="https://res.cloudinary.com/datacom-cabling/video/upload/f_auto,q_65/v1634019094/hero/Cabling-Vids-1--crop_sor0c1.mp4"
		alt="slow pan over ethernet cables"
	>
		<track kind="captions" />
	</video>
	{#if pageLoaded}
		<svg
			class="hero-circle"
			height={circleHeight}
			viewBox="0 0 396 396"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path
				in:draw={{ duration: 1200 }}
				d="M395.5 198C395.5 307.076 307.076 395.5 198 395.5C88.9238 395.5 0.5 307.076 0.5 198C0.5 88.9238 88.9238 0.5 198 0.5C307.076 0.5 395.5 88.9238 395.5 198Z"
				stroke="#F5DA4E"
			/>
		</svg>
	{/if}
	<div class="left-content">
		<div class="bglogo-wrap">
			<BGLogo />
		</div>
		<SectionHeader titleMainColor="Cabling <br> Service & <br> Expertise." />
		<p class="text">
			Datacom is your comprehensive solution for cabling services from fiber optic networking to
			video security.
		</p>
		<RingButton link="/#services" />
	</div>
	<svg
		class="left"
		id="Layer_1"
		data-name="Layer 1"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 0 1260 1500"
		bind:this={svgEl}
	>
		<path
			d="M1000,1609V3109H2260V2646.5c-157.72,0-287.5-129.78-287.5-287.5s129.78-287.5,287.5-287.5V1609Z"
			transform="translate(-1000 -1609)"
		/>
	</svg>
	<div class="right" />
	<div class="center">
		<h1>Your structured cabling <span class="accent">solution.</span></h1>
		<DiscButton />
	</div>
	<div class="arrow-mobile" on:click={scrollToServices}>
		<Arrow filled />
	</div>
</section>

<!-- <Loading /> -->
<style lang="scss">
	.loading {
		height: 100vh;
		width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: var(--white);
	}
	.hero {
		position: relative;
		height: 101vh;
		width: 100vw;
		display: flex;
		justify-content: center;
		align-items: center;
		flex: 1;
		&-vid {
			z-index: var(--base-one);
			position: absolute;
			top: 0;
			right: 0;
			height: 100%;
			width: 100%;
			opacity: 0;
			opacity: 0.5;
			transform: rotateY(180deg) scale(1.75) translate(-10vw, 0);
			transition: opacity 2s ease-in-out;
			@media (max-width: 1024px) {
				transform: rotateY(180deg) scale(2) translate(20vw, 0);
			}
		}
	}
	.left {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-100%, -50%);
		min-width: 52vw;
		min-height: 102vh;
		background-color: transparent;
		fill: white;
		@media (max-width: 1024px) {
			display: none;
		}
		/* background-image: url('/cut-out.png'); */
	}
	.left-content {
		z-index: var(--level-one);
		position: absolute;
		bottom: 17.5%;
		left: 15%;
		transform: scale(1.1);
		@media (max-width: 1024px) {
			display: none;
		}
		.bglogo-wrap {
			z-index: var(--base-one);
			position: absolute;
			bottom: -20vh;
			left: -27vh;
		}
		.text {
			margin-top: var(--title-margin);
			color: var(--text-color);
			width: 25%;
		}
	}
	.right {
		height: 100%;
		width: 100%;
		background-color: var(--primary-tr1);
	}
	.hero-circle {
		z-index: var(--level-eight);
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%) rotate(-0.25turn);
		@media (max-width: 1024px) {
			height: 42vh;
		}
	}
	.center {
		z-index: var(--level-eight);
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-59%, -50%);
		width: 20vh;
		color: var(--white);
		@media (max-width: 1025px) {
			transform: translate(-59%, -50%) scale(0.8);
		}
		h1 {
			margin: 0;
			text-align: left;
			line-height: 110%;
			letter-spacing: 1.5px;
			font-size: var(--text-display);
			font-weight: 600;
			.accent {
				color: var(--accent-color);
			}
		}
		.disc-button {
			z-index: var(--level-one);
			cursor: pointer;
			position: relative;
			margin-top: 1rem;
			padding-left: 1rem;
			font-size: var(--text-xl);
			font-weight: 700;
			color: var(--white);
			background-color: transparent;
			border: none;
			&:hover {
				.disc {
					transform: translate(-5%, -45%) scale(1.1);
				}
			}
			.disc {
				z-index: var(--base-one);
				position: absolute;
				top: 50%;
				left: 0;
				transform: translate(-5%, -45%);
				height: var(--circle-med);
				width: var(--circle-med);
				height: 40px;
				width: 40px;
				background-color: var(--accent-tr1);
				border-radius: var(--radius-rounded);
			}
		}
	}
	.arrow-mobile {
		display: none;
		z-index: var(--level-one);
		position: absolute;
		bottom: var(--vp-md);
		left: 50%;
		transform: translateX(-50%) scale(0.6) rotate(-90deg);
		opacity: 0.2;
		animation: 1.5s infinite alternate ease-out pulse;
		@media (max-width: 1024px) {
			display: unset;
		}
	}
	@keyframes pulse {
		from {
			opacity: 0.2;
		}
		to {
			opacity: 0.8;
		}
	}
</style>
