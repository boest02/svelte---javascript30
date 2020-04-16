
<script>
	let base = '#ffc600';
    let spacing = 10;
	let blur = 10;

	$: { console.log( "color: " + base + " spacing: " + spacing + " blur: " + blur);}
	
</script>

<main>
	<section>
		<h2>Update CSS Variables with <span class='hl'>JS</span></h2>

		<div class="controls">
			<label for="spacing">Spacing:</label>
			<input id="spacing" type="range" name="spacing" min="10" max="200" bind:value={spacing} data-sizing="px">

			<label for="blur">Blur:</label>
			<input id="blur" type="range" name="blur" min="0" max="25" bind:value={blur} data-sizing="px">

			<label for="base">Base Color</label>
			<input id="base" type="color" name="base" bind:value={base}>
		</div>

		<img src="https://source.unsplash.com/7bwQXzbF6KE/800x500"
			 style="--base: {base}; --spacing: {spacing + 'px'}; --blur: {blur + 'px'};">

	</section>
</main>

<style>

    img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }

    .hl {
      color: var(--base);
    }

    /*
      misc styles, nothing to do with CSS variables
    */

    main {
      text-align: center;
      background: #193549;
      color: white;
      font-family: 'helvetica neue', sans-serif;
      font-weight: 100;
      font-size: 50px;
    }

    .controls {
      margin-bottom: 50px;
    }

    input {
      width: 100px;
    }
</style>

