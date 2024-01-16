<script>
	import Introduction from '$lib/components/Introduction.svelte';
</script>

<main class="h-screen snap-y snap-mandatory overflow-y-auto scroll-smooth">
	<section id="about-me" class="snap-start min-h-screen flex flex-wrap items-center justify-center relative gap-4 p-4">
		<div class="sm:w-1/2 lg:w-1/3">
			<Introduction />
		</div>

		<div class="flex justify-center items-center absolute bottom-6 w-full">
			<a href="#home">HOME</a>
		</div>
	</section>

	<!-- <section id="home" class="snap-start min-h-screen flex flex-wrap items-center justify-center relative gap-4 p-4">
		<div class="sm:w-1/2 lg:w-1/3">
			<Introduction />
		</div>

		<div class="flex justify-center items-center absolute top-6 w-full">
			<a href="#about-me">About Me</a>
		</div>
	</section> -->
</main>
