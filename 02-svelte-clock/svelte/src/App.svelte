
<script>
	import { onMount } from 'svelte';


	let time = new Date();

	// these automatically update when `time`
	// changes, because of the `$:` prefix
	// these automatically update when `time`
	// changes, because of the `$:` prefix
	$: hours = time.getHours();
	$: minutes = time.getMinutes();
	$: seconds = time.getSeconds();

	onMount(() => {
		const interval = setInterval(() => {
			time = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<main>
	<section>
		<svg viewBox='-50 -50 100 100'>
			<circle class='clock-face' r='48'/>

			<!-- markers -->
			{#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minute}
				<line
					class='major'
					y1='35'
					y2='45'
					transform='rotate({30 * minute})'
				/>

				{#each [1, 2, 3, 4] as offset}
					<line
						class='minor'
						y1='42'
						y2='45'
						transform='rotate({6 * (minute + offset)})'
					/>
				{/each}
			{/each}

			<!-- hour hand -->
			<line
				class='hour'
				y1='2'
				y2='-20'
				transform='rotate({30 * hours + minutes / 2})'
			/>

			<!-- minute hand -->
			<line
				class='minute'
				y1='4'
				y2='-30'
				transform='rotate({6 * minutes + seconds / 10})'
			/>

			<!-- second hand -->
			<g transform='rotate({6 * seconds})'>
				<line class='second' y1='10' y2='-38'/>
				<line class='second-counterweight' y1='10' y2='2'/>
			</g>
		</svg>
	</section>
</main>

<style>
main {
	background: #018DED url(https://unsplash.it/1500/1000?image=881&blur=5);
	background-size: cover;
	font-family: 'helvetica neue';
	text-align: center;
	font-size: 10px;
}

section {
	margin: 0;
	font-size: 2rem;
	display: flex;
	flex: 1;
	min-height: 100vh;
	align-items: center;
}

svg {
	width: 80%;
	height: 80%;
	margin-left: 100px;
}

.clock-face {
	stroke: #333;
	fill: white;
}

.minor {
	stroke: #999;
	stroke-width: 0.5;
}

.major {
	stroke: #333;
	stroke-width: 1;
}

.hour {
	stroke: #333;
}

.minute {
	stroke: #666;
}

.second, .second-counterweight {
	stroke: rgb(180,0,0);
}

.second-counterweight {
	stroke-width: 3;
}
</style>

