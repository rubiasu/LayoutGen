<script>
	let cardRange = {min: 2, max: 99};
	let colRange = {min: 1, max: 12};
	let heightRange = {min: 2, max: 6}
	
	let cardCount = 2
	let columnCount = 3
	let maxHeight = 3
	$: fillers = calcFillers(cardCount);


	function calcFillers(cards) {
		return Math.floor(cards / 2 + 29)
	}

	function randSize(maxSize) {
		return Math.floor(Math.random() * maxSize) + 1
	}
</script>

<main>
  <div class="card">
    <h3 class="subtitle">Layout generator</h3>
    <h1>Settings</h1>
    
    <h3>{cardCount} cards (minus {fillers} fillers)</h3>
    <div class="form">
      <div class="input">
        {cardRange.min}
        <input class="slider" type="range" min={cardRange.min} max={cardRange.max} bind:value={cardCount}>
	      {cardRange.max}
      </div>
    </div>
    
    <h3>{columnCount} columns</h3>
		<div class=form>
	    <div class="input">
				{colRange.min}
				<input class="slider"  type="range" min={colRange.min} max={colRange.max} bind:value={columnCount}>
				{colRange.max}
	    </div>
				
			</div>
			<h3>Max Card Height: {maxHeight} </h3>
		<div class="form">
			<div class="input">
				{heightRange.min}
				<input class="slider" type="range" min={heightRange.min} max={heightRange.max} bind:value={maxHeight}>
				{heightRange.max}
			</div>
		</div>
  </div>
	
  <div class="grid" style="grid-template-columns: repeat({columnCount}, 1fr)">
		
		{#each Array(cardCount) as card}
			<div class="card" style="grid-column: span {randSize(columnCount)}; grid-row: span {randSize(maxHeight)};">
			</div>
		{/each}
		
		{#each Array(fillers) as card}
			<div class="card">
			</div>
		{/each}
		
	</div>
</main>

<style>
 main {
	 color: white;
	 margin: 0;
	 font-family: Arial;
	 width: 90%;
	 max-width: 1200px;
	 margin: 40px auto;
}
 .card {
	 padding: 20px;
	 border-radius: 4px;
	 background: #1a1a1a;
}
 .card .subtitle {
	 font-size: 1rem;
	 text-transform: uppercase;
	 color: #f96743;
	 margin-bottom: 0;
}
 .card h1 {
	 margin-top: 0.4em;
}
 .form {
	 width: 100%;
	 display: flex;
}
 .form .input {
	 width: 100%;
	 display: flex;
	 align-items: center;
	 font-weight: bold;
}
 input[type="range"] {
	 width: 100%;
	 margin: 0 20px;
	 -webkit-appearance: none;
	 appearance: none;
	 width: 100%;
	 height: 0.5rem;
	 background: #d3d3d3;
	 outline: none;
	 border-radius: 100px;
	 --thumb-bg: yellow;
}
 .slider::-webkit-slider-thumb {
	 -webkit-appearance: none;
	 appearance: none;
	 width: 1rem;
	 height: 1rem;
	 background: #4777d8;
	 cursor: pointer;
	 border-radius: 100%;
}
 h3 {
	 color: rgba(255, 255, 255, 0.5);
}
 .grid {
	 margin: 30px 0;
	 display: grid;
	 grid-template-columns: repeat(3, 1fr);
	 grid-gap: 10px;
	 grid-auto-flow: dense;
	 grid-auto-rows: 150px;
}
 .grid .card {
	 box-sizing: border-box;
	 height: 100%;
	 border: 0px solid #f96743;
	 transition: border-width 200ms;
}
 .grid .card:hover {
	 border-width: 2px;
}
 @media (max-width: 500px) {
	 .form {
		 flex-wrap: wrap;
	}
}
</style>