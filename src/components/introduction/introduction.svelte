<script>
import { onMount } from 'svelte';

onMount(() => {
    const no2 = document.getElementById('no2');
    const auto = document.getElementById('auto');
    const hoest = document.getElementById('schadelijk')


    // Function to recall to see if element is in viewport
    const elementInViewport = (el) => {
        let top = el.offsetTop;
        let left = el.offsetLeft;
        let width = el.offsetWidth;
        let height = el.offsetHeight;

        while (el.offsetParent) {
            el = el.offsetParent;
            top += el.offsetTop;
            left += el.offsetLeft;
        }

        return (
            top < (window.pageYOffset + window.innerHeight) &&
            left < (window.pageXOffset + window.innerWidth) &&
            (top + height) > window.pageYOffset &&
            (left + width) > window.pageXOffset
        );
    }


    window.onscroll = () => {
        if (elementInViewport(no2)) {
            no2.classList.add('jump');
        }

        if (elementInViewport(auto)) {
            auto.classList.add('jump');
        }

        if (elementInViewport(hoest)) {
            hoest.classList.add('jump-adem')
        }
    }
})
</script>

<style>
.introduction {
   position: relative;
   display: flex;
   flex-direction: column;
   justify-content: center;
   align-items: center;
   height: 80vh;
   background-color: #C9DADA;
}
.introduction h1 {
   font-size: 4rem;
   color: #587D71;
   margin-bottom: 2rem;
}
.circle {
   display: flex;
   justify-content: center;
   align-items: center;
   position: absolute;
   bottom: 50px;
   background-color: #587d71;
   height: 60px;
   width: 60px;
   border-radius: 50%;
}

svg {
   height: 1.4rem;
   fill: white;
}

.container {
   background-color: #F4F4F4;
   height: 50vh;
   display: flex;
   flex-direction: row;
   justify-content: center;
   align-items: center;
}

.text {
   width: 60%;
   padding: 0 10rem;
   max-width: 50em;
}

.text h2 {
   margin-bottom: 0.5rem;
}

#no2 {
   width: var(--plaatmaat);
   height: var(--plaatmaat);
   background: transparent url('../assets/introduction/no2.png') 0 0 no-repeat;
   background-size: cover;
   filter: drop-shadow(-30px 10px 4px rgba(0,0,0,0.3));
}

#auto {
   width: var(--plaatmaat);
   height: var(--plaatmaat);
   background: transparent url('../assets/introduction/auto.png') 0 0 no-repeat;
   background-size: cover;
   filter: drop-shadow(-30px 10px 4px rgba(0,0,0,0.3));
}

#schadelijk {
   width: var(--plaatmaat);
   height: var(--plaatmaat);
   background: transparent url('../assets/introduction/hoest.png') 0 0 no-repeat;
   background-size: cover;
   filter: drop-shadow(-30px 10px 4px rgba(0,0,0,0.3));
}


@media only screen and (max-width: 600px) {
   .introduction h1 {
      text-align: center;
      font-size: 2rem;
   }

  .container {
     flex-direction: column;
  }
  
  .text {
   width: 100%;
   padding: 40px;
}
}
</style>

<section class="introduction">
   <h1>Hoe een virus de lucht schoner maakte.</h1>
   <div class='circle'>
      <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
         viewBox="0 0 490.688 490.688" style="enable-background:new 0 0 490.688 490.688;" xml:space="preserve">
      <g>
         <path style="fill:#607D8B;" d="M472.328,216.529L245.213,443.665L18.098,216.529c-4.237-4.093-10.99-3.975-15.083,0.262
            c-3.992,4.134-3.992,10.687,0,14.82l234.667,234.667c4.165,4.164,10.917,4.164,15.083,0l234.667-234.667
            c4.093-4.237,3.975-10.99-0.262-15.083c-4.134-3.993-10.687-3.993-14.821,0L472.328,216.529z"/>
         <path style="fill:#607D8B;" d="M472.328,24.529L245.213,251.665L18.098,24.529c-4.237-4.093-10.99-3.975-15.083,0.262
            c-3.992,4.134-3.992,10.687,0,14.821l234.667,234.667c4.165,4.164,10.917,4.164,15.083,0L487.432,39.612
            c4.237-4.093,4.354-10.845,0.262-15.083c-4.093-4.237-10.845-4.354-15.083-0.262c-0.089,0.086-0.176,0.173-0.262,0.262
            L472.328,24.529z"/>
      </g>
      <path d="M245.213,469.415c-2.831,0.005-5.548-1.115-7.552-3.115L2.994,231.633c-4.093-4.237-3.975-10.99,0.262-15.083
         c4.134-3.992,10.687-3.992,14.82,0l227.136,227.115l227.115-227.136c4.237-4.093,10.99-3.975,15.083,0.262
         c3.993,4.134,3.993,10.687,0,14.821L252.744,466.279C250.748,468.28,248.04,469.408,245.213,469.415z"/>
      <path d="M245.213,277.415c-2.831,0.005-5.548-1.115-7.552-3.115L2.994,39.633c-4.093-4.237-3.975-10.99,0.262-15.083
         c4.134-3.992,10.687-3.992,14.821,0l227.136,227.115L472.328,24.529c4.093-4.237,10.845-4.354,15.083-0.262
         s4.354,10.845,0.262,15.083c-0.086,0.089-0.173,0.176-0.262,0.262L252.744,274.279C250.748,276.28,248.04,277.408,245.213,277.415z"
         />
   </div>
</section>

<section class="what__is__no2">
   <div class="container">
      <div id="no2"></div>
      <div class="text">
      <h2>Wat is No2?</h2>
		<p>NO2 of stikstofdioxide is een gas dat onstaat bij verschillende soorten verbrandingsprocessen. Bij hele hoge temperaturen onstaan er chemische reacties
         tusseen stikstof (N2) en zuurstof (O2). Hierbij onstaat er eerst stikstofmonoxide (NO) en door de verdere reactie met zuurstof ook stikstofdioxide (NO2).
      </p>
      </div>
   </div>
   <div class="container">
      <div class="text">
      <h2>Wat veroorzaakt No2?</h2>
		<p>NO2 wordt vooral veroorzaakt door verbrandingsprocessen door menselijke activiteiten, zoals het verbranden van fossiele brandstoffen (kolen, olie, aardgas, diesel, en benzine). Industrie, energiecentrales, scheepvaart en het wegverkeer zijn daardoor belangrijke sectoren voor de uitstoot van NO2 in Nederland.NO2 kan ook op natuurlijke wijze ontstaan, zoals bij bosbranden of door bliksem in de atmosfeer. Ook planten en bacteriën kunnen NO2 aanmaken in de bodem en in water.</p>
      </div>
      <div id="auto"></div>
   </div>
   <div class="container">
      <div id="schadelijk"></div>
      <div class="text">
      <h2>Waarom is NO2 schadelijk?</h2>
		<p>Stikstofdioxide is in grote hoeveelheid schadelijk voor de mens. Dat komt omdat doordringt tot de kleinste vertakkingen van de luchtwegen, daardoor gaan de longen minder goed werken. Mensen kunnen daardoor luchtwegklachten en astma-aanvallen krijgen.
         In de natuur zorgt NO2 ervoor dat de biodiversiteit afneemt, dit betekend dat er er veel soorten planten worden verdrongen door planten die goed groeien door NO2, zoals gras en brandnetels. Met het gevolg dat niet alleen planten uitsterven maar ook dieren.  
      </p>
      </div>
	</div>
</section>




 
 

