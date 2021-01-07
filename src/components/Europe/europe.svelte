<script>
	import { geoMercator, geoPath } from 'd3'
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
    const map = await fetch('https://gist.githubusercontent.com/milafrerichs/69035da4707ea51886eb/raw/4cb1783c2904f52cbb8a258ee96031f9054d155b/eu.topojson')
    
	const json = await map.json()
	console.log(json)
    const topoData = feature(json, json.objects.europe)
    const land = {
      ...topoData,
      features: topoData.features,
    }
    mapData = land.features
  })

</script>

<style>
svg {
	fill: hotpink;

}
</style>

<main>
	<svg width={width} height={height}>
		{#each mapData as feature}
		  <path
			d={path(feature)}
		  />
		{/each}
	  </svg>
</main>

