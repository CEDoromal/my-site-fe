<script lang="ts">
	import { onMount } from 'svelte';

	let className: string | undefined = undefined;
	export { className as class };
	export let quantity: number = 1;

	function getRndInteger(min: number, max: number) {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}

	let mousePosition = { x: 50, y: 50 };

	onMount(() => {
		document.addEventListener('mousemove', (event) => {
			mousePosition.x = event.pageX;
			mousePosition.y = event.pageY;
		});

		let fireflies = Array.from(
			document.getElementsByClassName('firefly') as HTMLCollectionOf<HTMLElement>
		);

		const fireflyUpdateArray: number[] = [];

		fireflies.forEach((firefly) => {
			const duration = getRndInteger(2000, 4000);
			firefly.style.transitionDuration = duration + 'ms';
			firefly.style.animationDuration = duration * 4 + 'ms';

			fireflyUpdateArray.push(
				setInterval(() => {
					const target = {
						x: mousePosition.x + getRndInteger(-200, 200),
						y: mousePosition.y + getRndInteger(-200, 200)
					};

					firefly.style.translate = target.x + 'px ' + target.y + 'px';
				}, duration)
			);
		});
	});
</script>

<div class={className}>
	<div class="relative flex h-full w-full items-center justify-center overflow-hidden">
		<div class="fireflies absolute left-0 top-0 h-full w-full">
			{#each { length: quantity } as _}
				<div class="firefly absolute animate-pulse mix-blend-lighten"></div>
			{/each}
		</div>
	</div>
</div>

<style>
	@keyframes pulse {
		50% {
			opacity: 0.5;
		}
	}
	.animate-pulse {
		animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
	}

	@keyframes firefly-animation {
		0%,
		100% {
			top: -150px;
			left: 0px;
			opacity: 1;
			scale: 100% 100%;
		}
		25% {
			left: 150px;
			opacity: 0;
			scale: 120% 120%;
		}
		50% {
			top: 150px;
			opacity: 1;
			scale: 100% 100%;
		}
		75% {
			left: -150px;
			opacity: 0;
			scale: 80% 80%;
		}
	}
	.firefly {
		box-shadow: 0 0 0.2vh 0.2vh greenyellow;
		transition-timing-function: ease-in-out;
		animation-name: firefly-animation;
		animation-timing-function: ease-in-out;
		animation-delay: 0;
		animation-iteration-count: infinite;
		animation-direction: alternate;
	}
</style>
