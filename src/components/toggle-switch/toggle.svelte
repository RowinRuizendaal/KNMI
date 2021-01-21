<!-- <script>
import { onMount, afterUpdate} from 'svelte'


export let hide;


let test = false;


onMount(() => {
    const toggle = document.getElementById('container');
    const toggleContainer = document.getElementById('toggle-container');
    let toggleNumber;
    
    toggle.addEventListener('click', function() {
	toggleNumber = !toggleNumber;
	if (toggleNumber) {
		toggleContainer.style.clipPath = 'inset(0 0 0 50%)';
		toggleContainer.style.backgroundColor = '#427468';
	} else {
		toggleContainer.style.clipPath = 'inset(0 50% 0 0)';
		toggleContainer.style.backgroundColor = '#427468';
	}
})
})

afterUpdate(() => {
    hide = test;
})

</script>

<style>
    a {
	text-decoration: none;
	opacity: .6;
	padding: 60px;
	font-weight: bolder;
	position: absolute;
	right: 0px;
	bottom: 0px;
	font-size: 1.4em;
}

a:hover {
	opacity: 1;
}

#container {
	width: 160px;
	height: 36px;
	margin: auto;
	position: relative;
	border-radius: 6px;
	overflow: hidden;
	user-select: none;
	cursor: pointer;
}

.inner-container {
	position: absolute;
	left: 0;
	top: 0;
	width: inherit;
	height: inherit;
	text-transform: uppercase;
	font-size: .6em;
	letter-spacing: .2em;
}

.inner-container:first-child {
	background: #e9e9e9;
	color: #a9a9a9;
}

.inner-container:nth-child(2) {
	background: #427468;
	color: white;
	clip-path: inset(0 50% 0 0);
	transition: .3s cubic-bezier(0,0,0,1);
}

.toggle {
	width: 50%;
	position: absolute;
	height: inherit;
	display: flex;
	box-sizing: border-box;
}

.toggle p {
	margin: auto;
}

.toggle:nth-child(1) {
	right: 0;
}
</style>

<p>{hide}</p>
<div id="container">
	<div class="inner-container">
		<div class="toggle" on:click={() => test = !test}>
			<p>Grafiek</p>
		</div>
		<div class="toggle" on:click={() => test = !test}>
			<p>Landkaart</p>
		</div>
	</div>
	<div class="inner-container" id='toggle-container'>
		<div class="toggle" on:click={() => test = !test}>
			<p>Grafiek</p>
		</div>
		<div class="toggle" on:click={() => test = !test}>
			<p>Landkaart</p>
		</div>
	</div>
</div> -->