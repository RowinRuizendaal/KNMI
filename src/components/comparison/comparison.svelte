<script>
import Lazy from 'svelte-lazy'
import { beforeUpdate, afterUpdate} from 'svelte'
import maatregelen from '../../store/messurements'
export let week;

$: weeknummer = week;


let messurement;

$: nederland = {
    'buiten' : false,
    'horeca' : false,
    'reizen' : false,
    'school' : false,
    'samenkomsten': false,
    'sport': false,
    'werk': false,
    'winkels': false,
    'bezoek': false
}

$: italie = {
    'buiten' : false,
    'horeca' : false,
    'reizen' : false,
    'school' : false,
    'samenkomsten': false,
    'sport': false,
    'werk': false,
    'winkels': false,
    'bezoek': false
}




const changeWeek = (nummer, land) => {
    let categoryLand;

    //Specify what country
    if (land === 'Nederland') {
        categoryLand = nederland
    } else {
        categoryLand = italie
    }

    // Return messurement based on week and land
    const findCategory = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.category)
    
    // update the specific land to false aka reset
    for (const i in categoryLand) {
        categoryLand[i] = false
        
    }
    // Find what category is going to glow and set it t true
    for (const i of findCategory) {
        categoryLand[i] = true
    }
    
     // Find what category is going to glow and set it t true  
    const findMeasure = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.maatregel)

    // If there are no messurement make sure to provide feedback     
    if (findMeasure.length === 0) {
        messurement = 'Geen data voor deze week | No data for this week'
    } else {
        messurement = findMeasure
    }
    return messurement
}

// Update the variable with them self
afterUpdate(() => {
    nederland = nederland;
    italie = italie;
})

</script>


<style>
.compare {
    margin-top: 2vh;
    position: relative;
    text-align: center;
}

.container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
}

.icons, .icons img {
    display: flex;
    justify-content: center;
    gap: 5px;
    margin-top: 2rem;
    align-items: center;
    flex-direction: row;
}

.picture-1 img,
.picture-2 img {
    height: 70vh;
}

.circle img {
    height: 40px;
    width: 40px;
    border-radius: 50%;
    background-color: #587d71;
    margin-bottom: 2rem;
}

.not-active {
    opacity: 0.5;
}

.active {
    opacity: 1;
    animation: maatregeladd 5s 1 forwards; 
}


@keyframes maatregelactivate {
	0% { transform: scale(1); opacity: 0.3; }
	50% { transform: scale(1.5); }
	100% { transform: scale(1); opacity: 1; }
}

@keyframes maatregeloff {
	0% { opacity: 1; transform: scale(1); }
	50% { transform: scale(0.5); opacity: 0.1; }
	100% { opacity: 0.3; }
}

@keyframes maatregeladd {
	0% { transform: scale(1); }
	12.5% { opacity: 1; }
	25% { opacity: 0.3; }
	37.5% { opacity: 1; }
	50% { transform: scale(1.5); opacity: 0.3; }
	62.5% { opacity: 1; }
	75% { opacity: 0.3; }
	100% { opacity: 1; }
}

@keyframes maatregelsubtract {
	0% { transform: scale(1); }
	12.5% { opacity: 1; }
	25% { opacity: 0.3; }
	37.5% { opacity: 1; }
	50% { transform: scale(0.5); opacity: 0.3; }
	62.5% { opacity: 1; }
	75% { opacity: 0.3; }
	100% { opacity: 1; }
}

</style>


<section class='compare'>
    <h2>Landen vergelijken week: {week}</h2>
    <div class="container">
       <div class="picture-1">
          <Lazy>
             <img src="./assets/comparison/nederland.svg" alt="nederland">
          </Lazy>
          <div class="icons">
             <div class="circle">
                <img class="{nederland.buiten ? 'active' : 'not-active'}" src="./assets/icons/buiten.svg" alt="buiten">
             </div>
             <div class="circle">
                <img class={nederland.horeca ? 'active' : 'not-active'} src="./assets/icons/horeca.svg" alt="horeca">
             </div>
             <div class="circle nederland-reizen">
                <img class={nederland.reizen ? 'active' : 'not-active'} src="./assets/icons/reizen.svg" alt="reizen">
             </div>
             <div class="circle">
                <img class={nederland.samenkomsten ? 'active' : 'not-active'} src="./assets/icons/samenkomsten.svg" alt="samenkomen">
             </div>
             <div class="circle">
                <img class={nederland.sport ? 'active' : 'not-active'} src="./assets/icons/sport.svg" alt="sport">
             </div>
             <div class="circle">
                <img class={nederland.werk ? 'active' : 'not-active'} src="./assets/icons/werk.svg" alt="werk">
             </div>
             <div class="circle">
                <img class={nederland.winkels ? 'active' : 'not-active'} src="./assets/icons/winkels.svg" alt="winkels">
             </div>
             <div class="circle">
                <img class={nederland.bezoek ? 'active' : 'not-active'} src="./assets/icons/bezoek.svg" alt="bezoek">
             </div>
          </div>
          <p>Nederland: {changeWeek(weeknummer, 'Nederland')}</p>
       </div>
       <div class="picture-2">
          <Lazy>
             <img src="./assets/comparison/nederland.svg" alt="nederland">
          </Lazy>
          <div class="icons">
             <div class="circle">
                <img class={italie.buiten ? 'active' : 'not-active'} src="./assets/icons/buiten.svg" alt="buiten">
             </div>
             <div class="circle">
                <img class={italie.horeca ? 'active' : 'not-active'} src="./assets/icons/horeca.svg" alt="horeca">
             </div>
             <div class="circle">
                <img class={italie.reizen ? 'active' : 'not-active'} src="./assets/icons/reizen.svg" alt="reizen">
             </div>
             <div class="circle">
                <img class={italie.samenkomsten ? 'active' : 'not-active'} src="./assets/icons/samenkomsten.svg" alt="samenkomen">
             </div>
             <div class="circle">
                <img class={italie.sport ? 'active' : 'not-active'} src="./assets/icons/sport.svg" alt="sport">
             </div>
             <div class="circle">
                <img class={italie.werk ? 'active' : 'not-active'} src="./assets/icons/werk.svg" alt="werk">
             </div>
             <div class="circle">
                <img class={italie.winkels ? 'active' : 'not-active'} src="./assets/icons/winkels.svg" alt="winkels">
             </div>
             <div class="circle">
                <img class={italie.bezoek ? 'active' : 'not-active'} src="./assets/icons/bezoek.svg" alt="bezoek">
             </div>
          </div>
          <p>Italie: {changeWeek(weeknummer, 'Italie')}</p>
       </div>
    </div>
 </section>
 