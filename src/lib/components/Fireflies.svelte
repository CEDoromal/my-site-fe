<script lang="ts">
	import { onMount } from 'svelte';

	let className: string | undefined = undefined;
	export { className as class };
	export let quantity: number = 1;

	function getRndInteger(min: number, max: number) {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}

	onMount(() => {
		const fireflies = document.getElementById('fireflies');
		
		let mouse = {
			position: {
				x: fireflies!.offsetWidth/2,
				y: fireflies!.offsetHeight/2
			}
		};

		document.addEventListener('mousemove', (event) => {
			mouse.position.x = event.pageX;
			mouse.position.y = event.pageY;
		});

		let fireflyArray = Array.from(
			document.getElementsByClassName('firefly') as HTMLCollectionOf<HTMLElement>
		);

		const fireflyUpdateArray: number[] = [];

		fireflyArray.forEach((firefly) => {
			const duration = getRndInteger(1500, 4000);
			firefly.style.transitionDuration = duration + 'ms';
			firefly.style.animationDuration = duration * 4 + 'ms';

			fireflyUpdateArray.push(
				setInterval(() => {
					const target = {
						x: mouse.position.x + getRndInteger(-200, 200),
						y: mouse.position.y + getRndInteger(-200, 200)
					};

					firefly.style.translate = target.x + 'px ' + target.y + 'px';
				}, duration)
			);
		});
	});
</script>

<div id="fireflies" class={className}>
	<div class="relative left-0 top-0 flex h-full w-full overflow-clip">
		{#each { length: quantity } as _}
			<div class="firefly absolute mix-blend-lighten"></div>
		{/each}
	</div>
</div>

<style>
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
		box-shadow: 0 0 0.2vh 0.2vh yellowgreen;
		transition-timing-function: ease-in-out;
		animation-name: firefly-animation;
		animation-timing-function: ease-in-out;
		animation-delay: 0;
		animation-iteration-count: infinite;
		animation-direction: alternate;
	}
</style>
