<script>
import Lazy from 'svelte-lazy'
import { onMount, afterUpdate} from 'svelte'
import maatregelen from '../../store/messurements'
export let week;

$: weeknummer = week;


let messurement;
let test = []

// Icons to be activated or not
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

// Text
$: textNederland = {
    'buiten' : '',
    'horeca' : '',
    'reizen' : '',
    'school' : '',
    'samenkomsten': '',
    'sport': '',
    'werk': '',
    'winkels': '',
    'bezoek': ''
}

$: textItalie = {
    'buiten' : '',
    'horeca' : '',
    'reizen' : '',
    'school' : '',
    'samenkomsten': '',
    'sport': '',
    'werk': '',
    'winkels': '',
    'bezoek': ''
}




const changeWeek = (nummer, land) => {
    let categoryLand;
    let text;

    //Specify what country
    if (land === 'Nederland') {
        categoryLand = nederland
        text = textNederland
    } else {
        categoryLand = italie
        text = textItalie
    }

    // Return messurement based on week and land
    const findCategory = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.category.toLocaleLowerCase())
    


    // update the specific land to false aka reset
    for (const i in categoryLand) {
        categoryLand[i] = false
        
    }


     // Find what category is going to glow and set it t true  
    const findMeasure = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.maatregel)

    // If there are no messurement make sure to provide feedback     
    if (findMeasure.length === 0) {
        messurement = 'Geen data voor deze week | No data for this week'
    } else {
       for (let i in findMeasure) {
         messurement = findMeasure
       }
    }

      if (land === 'Nederland') {
       // Find what category is going to glow and set it t true
       for (const i of findCategory) {
        categoryLand[i] = true
        textNederland[i]= messurement
        }
      } else if (land === 'Italie') {
         for (const i of findCategory) {
        categoryLand[i] = true
        textItalie[i] = messurement
        }
      }


    return messurement
}

const changeImage = (count) => {
    let nederland = `assets/comparison/effect-matregelen/nederland/week${count}.png`;
    let italie = `assets/comparison/effect-matregelen/italie/week${count}.png`

    document.getElementById('slider-nederland').src = nederland
    document.getElementById('slider-italie').src = italie
    }


// Update the variable with them self
afterUpdate(() => {
    nederland = nederland;
    italie = italie;
    textNederland = textNederland;
    changeImage(weeknummer)
})

onMount(() => {
   changeImage(weeknummer)
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
    gap: 5px;
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
    animation: var(--maatregel); 
}



.active:hover + .hide-div{
   display: block;
}




.hide-div {
   height: 10rem;
   width: 20rem;
   background-color: #587d71;
   color: white;
   display: none;
   position: absolute;
   top: 0;
}

.hide-div p {
   max-width: 100em;
}

.hide {
   display: none;
}


</style>


<section class='compare'>
    <h2>Landen vergelijken week: {week}</h2>
    <div class="container">
       <div class="picture-1">
          <Lazy>
            <img id='slider-nederland' src='assets/comparison/effect-matregelen/italie/week1.png' alt='NO2 uitstoot'>
          </Lazy>
          <div class="icons">
             <div class="circle">
                <img class="{nederland.buiten ? 'active' : 'not-active'}" src="./assets/Icons/buiten.svg" alt="buiten">
                <div class="{nederland.buiten ? 'hide-div': 'hide'}">
                  <h4>Maatregelen buiten</h4>
                  <p>{textNederland.buiten}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.horeca ? 'active' : 'not-active'} src="./assets/Icons/horeca.svg" alt="horeca">
                <div class="{nederland.horeca ? 'hide-div': 'hide'}">
                  <h4>Maatregelen horeca</h4>
                  <p>{textNederland.horeca}</p>
               </div>
             </div>
             <div class="circle nederland-reizen">
                <img class={nederland.reizen ? 'active' : 'not-active'} src="./assets/Icons/reizen.svg" alt="reizen">
                <div class="{nederland.reizen ? 'hide-div': 'hide'}">
                  <h4>Maatregelen reizen</h4>
                  <p>{textNederland.reizen}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.samenkomsten ? 'active' : 'not-active'} src="./assets/Icons/samenkomsten.svg" alt="samenkomen">
                <div class="{nederland.samenkomsten ? 'hide-div': 'hide'}">
                  <h4>Maatregelen samenkomsten</h4>
                  <p>{textNederland.samenkomsten}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.sport ? 'active' : 'not-active'} src="./assets/Icons/sport.svg" alt="sport">
                <div class="{nederland.sport ? 'hide-div': 'hide'}">
                  <h4>Maatregelen sport</h4>
                  <p>{textNederland.sport}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.werk ? 'active' : 'not-active'} src="./assets/Icons/werk.svg" alt="werk">
                <div class="{nederland.werk ? 'hide-div': 'hide'}">
                  <h4>Maatregelen werk</h4>
                  <p>{textNederland.werk}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.winkels ? 'active' : 'not-active'} src="./assets/Icons/winkels.svg" alt="winkels">
                <div class="{nederland.winkels ? 'hide-div': 'hide'}">
                  <h4>Maatregelen winkels</h4>
                  <p>{textNederland.winkels}</p>
               </div>
             </div>
             <div class="circle">
                <img class={nederland.bezoek ? 'active' : 'not-active'} src="./assets/Icons/bezoek.svg" alt="bezoek">
                <div class="{nederland.bezoek ? 'hide-div': 'hide'}">
                  <h4>Maatregelen bezoek</h4>
                  <p>{textNederland.bezoek}</p>
               </div>
             </div>
          </div>
          <p class="hide">Nederland: {changeWeek(weeknummer, 'Nederland')}</p>
       </div>
       <div class="picture-2">
          <Lazy>
            <img id='slider-italie' src='assets/comparison/effect-matregelen/italie/week1.png' alt='NO2 uitstoot'>
          </Lazy>
          <div class="icons">
             <div class="circle">
                <img class={italie.buiten ? 'active' : 'not-active'} src="./assets/Icons/buiten.svg" alt="buiten">
                <div class="{italie.buiten ? 'hide-div': 'hide'}">
                  <h4>Maatregelen buiten</h4>
                  <p>{textItalie.buiten}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.horeca ? 'active' : 'not-active'} src="./assets/Icons/horeca.svg" alt="horeca">
                <div class="{italie.horeca ? 'hide-div': 'hide'}">
                  <h4>Maatregelen horeca</h4>
                  <p>{textItalie.horeca}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.reizen ? 'active' : 'not-active'} src="./assets/Icons/reizen.svg" alt="reizen">
                <div class="{italie.reizen ? 'hide-div': 'hide'}">
                  <h4>Maatregelen reizen</h4>
                  <p>{textItalie.reizen}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.samenkomsten ? 'active' : 'not-active'} src="./assets/Icons/samenkomsten.svg" alt="samenkomen">
                <div class="{italie.samenkomsten ? 'hide-div': 'hide'}">
                  <h4>Maatregelen samenkomsten</h4>
                  <p>{textItalie.samenkomsten}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.sport ? 'active' : 'not-active'} src="./assets/Icons/sport.svg" alt="sport">
                <div class="{italie.sport ? 'hide-div': 'hide'}">
                  <h4>Maatregelen sport</h4>
                  <p>{textItalie.sport}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.werk ? 'active' : 'not-active'} src="./assets/Icons/werk.svg" alt="werk">
                <div class="{italie.werk ? 'hide-div': 'hide'}">
                  <h4>Maatregelen werk</h4>
                  <p>{textItalie.werk}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.winkels ? 'active' : 'not-active'} src="./assets/Icons/winkels.svg" alt="winkels">
                <div class="{italie.winkels ? 'hide-div': 'hide'}">
                  <h4>Maatregelen winkels</h4>
                  <p>{textItalie.winkels}</p>
               </div>
             </div>
             <div class="circle">
                <img class={italie.bezoek ? 'active' : 'not-active'} src="./assets/Icons/bezoek.svg" alt="bezoek">
                <div class="{italie.bezoek ? 'hide-div': 'hide'}">
                  <h4>Maatregelen bezoek</h4>
                  <p>{textItalie.bezoek}</p>
               </div>
             </div>
          </div>
          <p class="hide">Italie: {changeWeek(weeknummer, 'Italie')}</p>
       </div>
    </div>
 </section>
 