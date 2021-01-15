<script>
import Lazy from 'svelte-lazy'
import maatregelen from '../../store/messurements'
export let week;

$: weeknummer = week;

let messurement;

const changeWeek = (nummer, land) => {

    let categoryLand;

    if (land === 'Nederland') {
        categoryLand = 'Nederland'
    } else {
        categoryLand = 'Italie'
    }
    const findCategory = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.category)
    
    category(findCategory, categoryLand)

    const findMeasure = maatregelen.filter(d => d.week === nummer && d.land === land)
        .map(d => d.maatregel)


    if (findMeasure.length === 0) {
        messurement = 'Geen data voor deze week | No data for this week'
    } else {
        messurement = findMeasure
    }

    return messurement

}

const category = (data, land) => {
    data.push(land)
    console.log(data)
}

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
                <img src="./assets/icons/buiten.svg" alt="buiten">
             </div>
             <div class="circle">
                <img src="./assets/icons/horeca.svg" alt="horeca">
             </div>
             <div class="circle">
                <img src="./assets/icons/reizen.svg" alt="reizen">
             </div>
             <div class="circle">
                <img src="./assets/icons/samenkomsten.svg" alt="samenkomen">
             </div>
             <div class="circle">
                <img src="./assets/icons/sport.svg" alt="sport">
             </div>
             <div class="circle">
                <img src="./assets/icons/werk.svg" alt="werk">
             </div>
             <div class="circle">
                <img src="./assets/icons/winkels.svg" alt="winkels">
             </div>
             <div class="circle">
                <img src="./assets/icons/bezoek.svg" alt="bezoek">
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
                <img src="./assets/icons/buiten.svg" alt="buiten">
             </div>
             <div class="circle">
                <img src="./assets/icons/horeca.svg" alt="horeca">
             </div>
             <div class="circle">
                <img src="./assets/icons/reizen.svg" alt="reizen">
             </div>
             <div class="circle">
                <img src="./assets/icons/samenkomsten.svg" alt="samenkomen">
             </div>
             <div class="circle">
                <img src="./assets/icons/sport.svg" alt="sport">
             </div>
             <div class="circle">
                <img src="./assets/icons/werk.svg" alt="werk">
             </div>
             <div class="circle">
                <img src="./assets/icons/winkels.svg" alt="winkels">
             </div>
             <div class="circle">
                <img src="./assets/icons/bezoek.svg" alt="bezoek">
             </div>
          </div>
          <p>Italie: {changeWeek(weeknummer, 'Italie')}</p>
       </div>
    </div>
 </section>
 