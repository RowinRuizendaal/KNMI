<script>
	import Header from './components/header/header.svelte'
	import Introduction from './components/introduction/introduction.svelte'
	import Imageslider from './components/Europe/europe-image-slider.svelte'
	import Europe from './components/Europe/europe-clickable.svelte'
	import Comparison from './components/comparison/comparison.svelte'
	import Chart from './components/chart/chartjs.svelte'


	let leeg = [];
	const test = async () => {
		const data = await (await fetch('./dataset/Netherlands.json')).json();
		data.map((d) => {
			leeg.push(d.number)
		})
		leeg = data
	}
	console.log(leeg)

</script>

<style>
</style>

<Header />
<main>
<Introduction />
<Imageslider />
<Comparison />
	{#await test()}
	<p>Loading... filter data</p>
	{:then data}
	<Chart data={data} getal={20}/>
	{/await}
</main>

