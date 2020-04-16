<script>
	import keys from './keys.js';
	import Key from './Key.svelte';

	import { tick } from 'svelte';

	const removeTransition = (e) => {
		if (e.propertyName !== 'transform') return;
		e.target.classList.remove('playing');
	}

  	const playSound = (e) => {
		const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
		const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
		if (!audio) return;
		key.classList.add('playing');
		audio.currentTime = 0;
		audio.play();
    }

    const setup = async () => {
        await tick();
        const keyElements = Array.from(document.querySelectorAll('.key'));
		keyElements.forEach(key => key.addEventListener('transitionend', removeTransition));
		window.addEventListener('keydown', playSound);
    }

    setup();

</script>

<main>
	<section>
		<div class="keys">
			{#each keys as key}
				<Key data={key.data} key={key.key} sound={key.sound} />
    		{/each}
  		</div>
	</section>
</main>

{#each keys as key}
	<audio data-key="{key.data}" src="{key.file}"></audio>
{/each}
  
<style>
main {
  font-size: 10px;
  background: url(https://i.imgur.com/b9r5sEL.jpg) bottom center;
  background-size: cover;
}

section, main {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

.keys {
  display: flex;
  flex: 1;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
}
</style>