<script>
	import Introduction from '$lib/components/Introduction.svelte';
	import { ChevronDown } from 'radix-icons-svelte';
	import { Button } from '$lib/components/ui/button';
</script>

<svelte:head>
	<title>CEDoromal</title>
</svelte:head>

<main class="h-screen snap-y snap-mandatory overflow-y-auto scroll-smooth">
	<section id="about-me">
		<Introduction class="sm:w-1/2 lg:w-1/3" />

		<div class="absolute bottom-16 flex w-full items-center justify-center">
			<Button href="#menu" size="icon" class="animate-bounce">
				<ChevronDown />
			</Button>
		</div>
	</section>

	<section id="menu">
		<Button href="#about-me" class="min-w-24">About Me</Button>
		<Button
			on:click={() => window.open('https://github.com/CEDoromal?tab=repositories', '_blank')}
			class="min-w-24">Projects</Button
		>
		<Button
			on:click={() => window.open('https://cedoromal.pages.dev/Doromal_Resume.pdf', '_blank')}
			class="min-w-24">Resume</Button
		>
	</section>
</main>

<style lang="postcss">
	section {
		@apply relative flex min-h-screen snap-start flex-col flex-wrap items-center justify-center gap-4 p-4;
	}
</style>
