<script>
	// your script goes here
	import Container from '$lib/containers/Container.svelte';
	import SectionHeader from '$lib/SectionHeader.svelte';
</script>

<!-- markup (zero or more items) goes here -->
<section class="about" id="about">
	<img class="bg-image" src="https://res.cloudinary.com/datacom-cabling/image/upload/f_auto,q_80/v1633947587/about/job-site_qgzuzc.jpg" alt="Construction site planning" />
	<Container column>
		<div class="about-inner">
			<SectionHeader mainColor="var(--white)" sub={'WHO WE ARE'} titleMainColor={'focus &'} titleYellow={'specialties'} />
			<p class="about-text">
				Datacom llc. is a Texas-based information technology solutions provider
				offering a wide range of IT expertise. Our focus is in network security, application
				delivery and IT infrastructure. Our goal is to provide industry leading IT solutions to help
				your organization improve network performance, mitigate risk and operate efficiently. 
        <br>
        <br>
        If your company needs access to specialized, highly-technical engineers for complex IT projects
				and/or emerging technologies, CTC Technologies is here to help. Whether it's a multi-site
				network refresh, large-scale wireless site survey, or a global SD-WAN implementation, we've
				got the proven experience to get your next IT project executed without having to hire
				additional employees or project managers.
			</p>
		</div>
	</Container>
</section>

<style lang="scss">
	.about {
		position: relative;
		height: 100vh;
		width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
		@media (max-width: 1024px) {
			height: max-content;
			padding: var(--mobile-sec-margin) 0;
		}
		&::before {
			z-index: var(--level-one);
			content: '';
			position: absolute;
			top: 0;
			left: 0;
			height: 100%;
			width: 100%;
			background: var(--primary-tr1);
		}
		&::after {
			z-index: var(--level-two);
			content: '';
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			height: 80vh;
			width: 80vh;
			border-radius: var(--radius-rounded);
			background: var(--barely-grey-tr1);
			@media (max-width: 1024px) {
				height: 42vh;
				width: 42vh;
			}
		}
		.bg-image {
      position: absolute;
      top: 0;
      left: 0;
			height: 100%;
			width: 100%;
			object-fit: cover;
			object-position: center;
			filter: saturate(0);
			@media (max-width: 1024px) {
			}
		}
		.about-inner {
      z-index: var(--level-three);
			height: 100%;
			width: calc(100% - var(--vp-lg));
      padding: 0 var(--vp-lg);
			display: flex;
			flex-direction: column;
			align-items: flex-start;
			justify-content: center;
      /* background-color: aqua; */
			@media (max-width: 1024px) {
				width: 90vw;
				padding: 5vw;
			}
		}
    .about-text {
      margin-top: var(--space-2xl);
      font-size: var(--text-xl);
      color: var(--white);
    }
	}
</style>
