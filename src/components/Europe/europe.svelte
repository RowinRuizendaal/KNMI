<script>
	import { geoMercator, geoPath, interpolateViridis } from 'd3'
  	import { onMount } from 'svelte'
	import { feature } from 'topojson'

	let mapData = []
	const width = 1000;
	const height = 800;
    const center = [5, 70]
    const scale = 600;
    
	const projection = geoMercator().scale(scale).translate([width / 2, 0]).center(center)
	const path = geoPath().projection(projection)
	  
	onMount(async function () {
    const map = await fetch('https://raw.githubusercontent.com/deldersveld/topojson/master/continents/europe.json')
    
	const json = await map.json()
    const topoData = feature(json, json.objects.continent_Europe_subunits)
    const land = {
      ...topoData,
      features: topoData.features,
    }
    mapData = land.features
  })

  const colorscheme = (t) => {
    const randomColor = Math.floor(Math.random()*t).toString(16);
    return `#${randomColor}`;
  }

  let ammountColors = 16777215;
  let sliderValue = 0
</script>

<style>
</style>

<main>
    <svg width={width} height={height} viewBox={`0 0 ${width} ${height}`}>
        <g>
        {#each mapData as feature}
		  <path
            d={path(feature)}
            class={feature.properties.geounit}
            fill={colorscheme(ammountColors)}
		  />
        {/each}
        </g>
      </svg>
      
      <div class="slidecontainer">
        <input type="range" bind:value={sliderValue} on:change={() => ammountColors += 1}>
        <p>{sliderValue}</p>
      </div>
</main>

