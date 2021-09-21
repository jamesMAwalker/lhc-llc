<script>
	import { draw } from 'svelte/transition';

	let loaded = false;

	setTimeout(() => {
		loaded = true;
	}, 200);

	/*
	 TODO: Write an algorithm that can keep the svg circle within the same distance of the png cutout.  
	*/
</script>

<section class="hero">
	<video
		class="hero-vid"
		autoplay
		muted
		loop
		src="https://res.cloudinary.com/jameswalker-work/video/upload/q_60/v1632240871/cabling-vids_xitbot.mp4"
		alt="slow pan over ethernet cables"
	>
		<track kind="captions" />
	</video>
	{#if loaded}
		<svg
			class="hero-circle"
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
	<div class="left" />
	<div class="right" />
	<div class="center">
		<h1>Your structured cabling <span class="accent">solution.</span></h1>
		<div class="button">
			<span class="circle--fade" />
			learn more
		</div>
	</div>
</section>

<style lang="scss">
	.hero {
		position: relative;
		height: 101vh;
		width: 100vw;
		display: flex;
		justify-content: center;
		align-items: center;
		flex: 1;
		overflow: hidden;
		&-vid {
			z-index: -1;
			position: absolute;
			top: 0;
			left: 0;
			height: 100%;
			width: 100%;
			transform: rotateY(180deg) scale(1.75) translate(17vh, 15vh);
			transition: var(--transition-1-smooth);
			transition: all 2s ease-in-out;
		}
	}
	.left {
		position: absolute;
		top: 0;
		left: 0;
		height: 100%;
		width: 50%;
		background-color: transparent;
		background-position: right;
    background-size: 55vw;
		background-image: url('/cut-out.png');
	}
	.right {
		height: 100%;
		width: 100%;
		background-color: var(--primary-tr-1);
	}
	.hero-circle {
		z-index: 2;
		position: absolute;
		top: 50%;
		left: 50%;
		height: 47vh;
    height: calc((((75vw - 80vh) / 2) + 100vh) * .4);
		transform: translate(-50%, -50.05%) rotate(-0.25turn);
    @media (max-height: 950px) {
      /* transform: translate(-50%, -50.05%) scale(1) rotate(-0.25turn); */
    }
	}
	.center {
    z-index: 3;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-59%, -50%) scale(0.9);
		width: 20vh;
		color: var(--white);
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
		.button {
      z-index: 3;
			cursor: pointer;
			position: relative;
			margin-top: 1rem;
			padding-left: 1rem;
			font-size: var(--text-xl);
			font-weight: 600;
			&:hover {
				.circle--fade {
					transform: translate(-5%, -45%) scale(1.1);
				}
			}
			.circle--fade {
				z-index: -1;
				position: absolute;
				top: 50%;
				left: 0;
				transform: translate(-5%, -45%);
				height: var(--circle-med);
				width: var(--circle-med);
				height: 40px;
				width: 40px;
				background-color: var(--accent-tr-1);
				border-radius: var(--radius-rounded);
			}
		}
	}
</style>