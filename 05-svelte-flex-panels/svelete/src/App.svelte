
<script>
    import { onMount } from 'svelte';
    import Panel from './Panel.svelte';

    let panels = [
      ["Hey", "Let's", "Dance"],
      ["Give", "Take", "Recieve"],
      ["Experience", "It", "Today"],
      ["Give", "All", "You can"],
      ["Life", "In", "Motion"]
    ];

    onMount(async () => {
      const panels = document.querySelectorAll('.panel');
      console.log("panels = ", panels);

      panels.forEach(panel => panel.addEventListener('click', toggleOpen));
      panels.forEach(panel => panel.addEventListener('transitionend', toggleActive));
	  });

    function toggleOpen() {
      console.log('Hello', this.classList);
      this.classList.toggle('open');
    }

    function toggleActive(e) {
      console.log(e.propertyName);
      if (e.propertyName.includes('flex')) {
        this.classList.toggle('open-active');
      }
    }

    
  </script>

<main>
	<div class="panels">
    {#each panels as panel, count}
       <Panel {count} {panel}/>
    {/each}
  </div>
</main>

<style>

    main {
      text-align: center;
      background: #193549;
      color: white;
      font-family: 'helvetica neue', sans-serif;
      font-weight: 100;
      font-size: 50px;
    }
    .panels {
      min-height: 100vh;
      overflow: hidden;
      display: flex;
    }

</style>

