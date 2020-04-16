
<script>
import Table from './Table.svelte';
import Object from './Object.svelte';
import { tick } from 'svelte';

  let displayArray = [];
  let displayValue = "";
  let showTable = false;
  let showValue = false;
  let showObject = false;

	const inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
      { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
      { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
      { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
      { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
      { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
      { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },
      { first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 },
      { first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 },
      { first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },
      { first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },
      { first: 'Hanna', last: 'Hammarström', year: 1829, passed: 1909 }
    ];

    const people = ['Beck, Glenn', 'Becker, Carl', 'Beckett, Samuel', 
                    'Beddoes, Mick', 'Beecher, Henry', 'Beethoven, Ludwig', 
                    'Begin, Menachem', 'Belloc, Hilaire', 'Bellow, Saul', 
                    'Benchley, Robert', 'Benenson, Peter', 'Ben-Gurion, David', 
                    'Benjamin, Walter', 'Benn, Tony', 'Bennington, Chester', 
                    'Benson, Leana', 'Bent, Silas', 'Bentsen, Lloyd', 
                    'Berger, Ric', 'Bergman, Ingmar', 'Berio, Luciano', 
                    'Berle, Milton', 'Berlin, Irving', 'Berne, Eric', 
                    'Bernhard, Sandra', 'Berra, Yogi', 'Berry, Halle', 
                    'Berry, Wendell', 'Bethea, Erin', 'Bevan, Aneurin', 
                    'Bevel, Ken', 'Biden, Joseph', 'Bierce, Ambrose', 
                    'Biko, Steve', 'Billings, Josh', 'Biondo, Frank', 
                    'Birrell, Augustine', 'Black Elk', 'Blair, Robert', 
                    'Blair, Tony', 'Blake, William'];

    const resetWhatToShow = async () => {
      showTable = false;
      showValue = false;
      showObject = false;
      await tick();
    }
    // Array.prototype.filter()
    // 1. Filter the list of inventors for those who were born in the 1500's
    const showFirst = () => {
      resetWhatToShow();
      const fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));

      console.table(fifteen);
      displayArray = fifteen;
      showTable = true;
    }

    // Array.prototype.map()
    // 2. Give us an array of the inventor first and last names
    const showSecond = () => {
      resetWhatToShow();
      const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
      console.log(fullNames);
      displayArray = fullNames;
      showObject = true;
    }

    // Array.prototype.sort()
    // 3. Sort the inventors by birthdate, oldest to youngest
    // const ordered = inventors.sort(function(a, b) {
    //   if(a.year > b.year) {
    //     return 1;
    //   } else {
    //     return -1;
    //   }
    // });
    const showThird = () => {
      resetWhatToShow();
      const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1);
      console.table(ordered);
      displayArray = ordered;
      showTable = true;
    }

    // Array.prototype.reduce()
    // 4. How many years did all the inventors live?
    const showFourth = () => {
      resetWhatToShow();
      const totalYears = inventors.reduce((total, inventor) => {
        return total + (inventor.passed - inventor.year);
      }, 0);

      console.log(totalYears);
      displayValue = totalYears;
      showValue = true;
    }

    // 5. Sort the inventors by years lived
    const showFifth = () => {
      resetWhatToShow();
      const oldest = inventors.sort(function(a, b) {
        const lastInventor = a.passed - a.year;
        const nextInventor = b.passed - b.year;
        return lastInventor > nextInventor ? -1 : 1;
      });
      console.table(oldest);
      displayArray = oldest;
      showTable = true;
    }

    // 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name
    // https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris

    // const category = document.querySelector('.mw-category');
    // const links = Array.from(category.querySelectorAll('a'));
    // const de = links
    //             .map(link => link.textContent)
    //             .filter(streetName => streetName.includes('de'));

    // 7. sort Exercise
    // Sort the people alphabetically by last name
    const showSeventh = () => {
      resetWhatToShow();
      const alpha = people.sort((lastOne, nextOne) => {
        const [aLast, aFirst] = lastOne.split(', ');
        const [bLast, bFirst] = nextOne.split(', ');
        return aLast > bLast ? 1 : -1;
      });
      console.log(alpha);
      displayArray = alpha;
      showObject = true;
    }

    // 8. Reduce Exercise
    // Sum up the instances of each of these
    const showEigth = () => {
      resetWhatToShow();
      const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck', 'pogostick'];

      const transportation = data.reduce(function(obj, item) {
        if (!obj[item]) {
          obj[item] = 0;
        }
        obj[item]++;
        return obj;
      }, {});

      console.log(transportation);
      displayArray = transportation;
      showObject = true;
    }
	
</script>

<main>
	<section>
    <p>Hit the button to see results...</p>
		<p><em>Psst: have a look at the JavaScript Console too</em> 💁</p>
    <section class="buttons">
      <button on:click={showFirst}>Filter the list of inventors for those who were born in the 1500's</button>
      <button on:click={showSecond}>Give us an array of the inventor first and last names</button>
      <button on:click={showThird}>Sort the inventors by birthdate, oldest to youngest</button>
      <button on:click={showFourth}>How many years did all the inventors live?</button>
      <button on:click={showFifth}>Sort the inventors by years lived</button>
      <button on:click={showSeventh}>Sort the people alphabetically by last name</button>
      <button on:click={showEigth}>Sum up the instances of each</button>
    </section>
    {#if showTable}
       <Table bind:data={displayArray} />
    {/if}
    {#if showObject}
       <Object bind:data={displayArray} />
    {/if}
    {#if showValue}
      <div>{displayValue}</div>    
    {/if}
    
	</section>
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
    p {
      margin: 0px;
      padding: 10px;
      font-size: 30px;
    }
    em {
      font-size: 20px;
    }
    .buttons {
      display: flex;
      flex-direction: row;
      justify-content: center;
      margin-bottom: 15px;
    }
    button {
      border: 1px solid black;
      padding: 10px;
      font-size: 25px;
      border-radius: 5px;
      margin: 5px;
    }
</style>

