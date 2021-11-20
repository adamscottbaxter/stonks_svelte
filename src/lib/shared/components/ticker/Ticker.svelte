<script>
// import { get } from "http";



	export let symb = '';
  
  // let datapoints = []
  $: promise = getRandomNumber(symb);

  async function getRandomNumber(symbol) {
    console.log(symbol.length)
    if (symb.length > 0) {
      console.log('length greater than 0')
// const res = await fetch(`http://localhost:5000/yfin/${symb}`).then((res) => res.json());
      const res = await fetch(`http://localhost:5000/yfin/${symbol}`);
      const text = await res.json();
      

      if (res.ok) {
        console.dir(text)
        return text;
      } else {
        throw new Error('text');
      }
      return 8
    } else {
      console.log('length 0')
    }
    
	}

</script>

<div>

	<h3>Symbol: {symb}</h3>
  {#await promise}
	<p>...waiting</p>
{:then number}
  <p>{number}</p>
  {#each number as day}
    <p>{day.Date} - {day.Close} - {day["Adj Close"]}</p>
  {/each}




{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

</div>
