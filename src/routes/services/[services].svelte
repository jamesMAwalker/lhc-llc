<script>
	import { fade, draw } from 'svelte/transition';
	import { page } from '$app/stores'

	import ContactForm from '../../lib/ContactForm.svelte';
	import SectionHeader from '$lib/SectionHeader.svelte';
	import RingButton from '../../lib/buttons/ring-button.svelte';
	import Container from '$lib/containers/Container.svelte';
	import BGCircle from '$lib/background/BGCircle.svelte';

	import { services } from '$lib/_data/services.js'

	let loaded = false;
	let centerCircle;
	let currentService = 'data-facilities';

	$: console.log("page from services: ", $page)

	let {
		title,
		imgUrlFrag,
		heroHeader: hero,
		heroBlurb,
		infoHeader: info,
		infoBlurb,
		processList,
		contactHeader: contact,
		contactBlurb
	} = services[currentService];

	const handleScroll = (e) => {
		let size = e.target.scrollTop / 100;
		centerCircle.style.transform = `translate(-50%, -50%) scale(${1 + 0.9 * size})`;
	};

	setTimeout(() => {
		loaded = true;
	}, 200);
</script>

<section class="service-hero" transition:fade>
	<div class="left">
		<div class="blurb-container">
			<SectionHeader
				sub={hero.sub}
				titleMainColor={hero.mainColor}
				titleYellow={hero.accentColor}
			/>
			<p class="blurb">
				{@html heroBlurb}
			</p>
			<RingButton link="/services/#info" />
		</div>
	</div>
	<div class="right">
		{#if loaded}
			<svg
				class="hero-circle"
				height="46vh"
				viewBox="0 0 396 396"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
				transform="rotate(180)"
			>
				<path
					in:draw={{ delay: 500, duration: 1200 }}
					d="M395.5 198C395.5 307.076 307.076 395.5 198 395.5C88.9238 395.5 0.5 307.076 0.5 198C0.5 88.9238 88.9238 0.5 198 0.5C307.076 0.5 395.5 88.9238 395.5 198Z"
					stroke="#F5DA4E"
				/>
			</svg>
		{/if}
		<div class="image-circle">
			<div class="image-shade" />
			<img
				src={`https://res.cloudinary.com/datacom-cabling/image/upload/f_auto,q_75/v1633947679/services/${imgUrlFrag}`}
				alt={title}
				class="hero-img"
			/>
		</div>
	</div>
</section>
<section class="service-info" id="info">
	<Container>
		<div class="left">
			<SectionHeader
				sub={info.sub}
				titleMainColor={info.mainColor}
				titleYellow={info.accentColor}
			/>
			<p class="blurb">
				{@html infoBlurb}
			</p>
		</div>
		<div class="right" on:scroll={(e) => handleScroll(e)}>
			<div class="process-steps">
				{#each processList as { title, steps }, idx (title)}
					<div class="process-block">
						<h4 class="step-title"><span>0{idx + 1}&nbsp;</span>{title}</h4>
						<ul class="steps-list">
							{#each steps as step (step)}
								<li class="step">{step}</li>
							{/each}
						</ul>
					</div>
				{/each}
			</div>
		</div>
	</Container>
	<div class="bgcircle--scaling" bind:this={centerCircle} />
</section>
<section class="service-contact">
	<BGCircle />
	<Container jcsb>
		<div class="left">
			<SectionHeader
				sub={contact.sub}
				titleMainColor={contact.mainColor}
				titleYellow={contact.accentColor}
			/>
			<div class="blurb">
				{@html contactBlurb}
			</div>
			<div class="call">
				<span class="text">or call today</span>
				<span class="number">289 . 555 . 1234</span>
			</div>
		</div>
		<div class="right">
			<ContactForm />
		</div>
	</Container>
</section>

<style lang="scss">
	.service-hero {
		height: 100vh;
		width: 100vw;
		background-color: var(--white);
		display: flex;
		align-items: flex-start;
		justify-content: flex-start;
		@media (max-width: 1024px) {
			height: max-content;
			margin-top: var(--vp-2xl);
			flex-direction: column-reverse;
		}
		.hero-circle {
			path {
				stroke-dashoffset: 78.5%;
			}
			@media (max-width: 1024px) {
				position: absolute;
				top: 50% !important	;
			}
		}
		.left {
			height: 100vh;
			width: 62vw;
			background-color: var(--white);
			display: flex;
			align-items: center;
			justify-content: center;
			@media (max-width: 1024px) {
				width: 100vw;
				height: max-content;
				padding-top: var(--vp-md);
				align-items: flex-start;
			}
		}
		.right {
			position: relative;
			height: 100vh;
			width: 38vw;
			background-color: var(--deep-cyan-tr);
			@media (max-width: 1024px) {
				height: 40vh;
				width: 100vw;
				background-color: var(--white);
				display: flex;
				align-items: center;
				justify-content: center;
			}
			.image-circle {
				position: absolute;
				height: 42vh;
				width: 42vh;
				top: 50%;
				left: 0%;
				transform: translate(-50%, -50%);
				border-radius: var(--radius-rounded);
				border: 2px solid var(--barely-grey);
				overflow: hidden;
				@media (max-width: 1024px) {
					top: 0;
					left: 0;
					position: relative;
					transform: translate(0, 0);
					height: 37.5vh;
					width: 37.5vh;
				}
			}
			.image-shade {
				position: absolute;
				height: 100%;
				width: 100%;
				background-color: var(--primary-tr2);
			}
			.hero-img {
				height: 110%;
				width: 110%;
				object-fit: cover;
				object-position: right;
			}
			.hero-circle {
				position: absolute;
				top: 50%;
				left: 0%;
				transform: translate(-50%, -50%);
				@media (max-width: 1024px) {
					top: 25%;
					left: 50%;
					height: 39vh;
					width: 39vh;
				}
			}
		}
		.blurb-container {
			height: 60%;
			width: 50%;
			display: flex;
			flex-direction: column;
			align-items: flex-start;
			justify-content: center;
			@media (max-width: 1024px) {
				width: 90vw;
				margin-bottom: var(--vp-xl);
			}
			.blurb {
				margin-top: var(--title-margin);
				margin-bottom: var(--space-lg);
				width: 75%;
				@media (max-width: 1024px) {
					width: 100%;
				}
			}
		}
	}
	:global(.service-info .container) {
		@media (max-width: 1024px) {
			flex-direction: column;
			align-items: center;
			justify-content: flex-start;
		}
	}
	.service-info {
		overflow: hidden;
		position: relative;
		height: 100vh;
		width: 100vw;
		background-color: var(--deep-cyan-tr3);
		display: flex;
		align-items: center;
		justify-content: center;
		@media (max-width: 1024px) {
			height: max-content;
		}
		.left {
			height: 100vh;
			width: 40%;
			padding-left: 10%;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: flex-start;
			background-color: var(--primary-tr1);
			background-color: transparent;
			@media (max-width: 1024px) {
				height: max-content;
				width: 90vw;
				margin-top: var(--vp-xl);
				justify-content: flex-start;
			}
		}
		.right {
			width: 50%;
			height: 100vh;
			background-color: transparent;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: flex-start;
			overflow: scroll;
			&::-webkit-scrollbar {
				display: none;
			}
			@media (max-width: 1024px) {
				width: 90vw;
				/* overflow: visible; */
				height: max-content;
			}
			.process-block {
				display: flex;
				flex-direction: column;
				align-items: flex-start;
				justify-content: space-evenly;
			}
			.process-steps {
				padding-top: var(--vp-lg);
				display: flex;
				flex-direction: column;
				align-items: flex-start;
				justify-content: center;
			}
			.steps-list {
				@media (max-width: 1024px) {
					margin-left: 5vw;
				}
			}
			.step-title {
				margin-top: var(--title-margin);
				color: var(--primary-color);
				font-size: var(--text-xl);
				text-transform: uppercase;
				span {
					font-size: var(--text-3xl);
					color: var(--primary-tr1);
				}
			}
			.step {
				color: var(--primary-tr1);
				font-size: var(--text-lg);
				/* font-weight: var(--semibold); */
				margin-bottom: var(--space-xl);
				text-transform: uppercase;
			}
		}
		.blurb {
			margin-top: var(--title-margin);
			width: 90%;
			color: var(--text-color);
		}
		.bgcircle--scaling {
			z-index: var(--base-one);
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			height: 20vh;
			width: 20vh;
			background-color: var(--primary-tr2);
			border-radius: var(--radius-rounded);
			transform-origin: center;
			transition: var(--transition-1-smooth);
			@media (max-width: 1024px) {
				display: none;
			}
		}
	}

	:global(.service-contact .container) {
		@media (max-width: 1024px) {
			height: max-content;
			flex-direction: column;
			align-items: center;
		}
	}
	.service-contact {
		position: relative;
		height: 120vh;
		width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
		@media (max-width: 1024px) {
			height: max-content;
		}
		.left {
			height: calc(70vh - var(--vp-lg));
			width: 30vw;
			margin-right: var(--block-center-margin);
			display: flex;
			flex-direction: column;
			align-items: start;
			justify-content: space-between;
			background-color: transparent;
			@media (max-width: 1024px) {
				height: max-content;
				width: 80vw;
				margin: var(--vp-xl) 0;
			}
			.blurb {
				margin-top: var(--title-margin);
				font-size: var(--text-lg);
				color: var(--text-color);
			}
			.call {
				margin-top: var(--space-3xl);
				display: flex;
				flex-direction: column;
				align-items: flex-start;
				justify-content: center;
				font-size: var(--text-2xl);
				font-weight: var(--bold);
				.text {
					color: var(--text-color);
					margin-bottom: var(--space-lg);
				}
				.number {
					color: var(--accent-color);
				}
			}
		}
		.right {
			height: 70vh;
			width: 55vw;
			background-color: transparent;
			@media (max-width: 1024px) {
				width: 80vw;
				height: max-content;
				margin-bottom: var(--vp-xl);
			}
		}
	}
	:global(.service-contact svg) {
		position: absolute;
		z-index: var(--base-one);
		top: 17.5vh;
		left: 15vw;
		transform: scale(1.3);
	}
</style>
