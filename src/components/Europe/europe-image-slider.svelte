<script>
    import Compare from '../comparison/comparison.svelte'

    const changeImage = (count) => {
    let src = `assets/slider/week${count}.png`
    document.getElementById('slider').src = src
    }

    let currentImage = 1


</script>

<style>
.slidecontainer {
    margin-top: 4rem;
    align-items: center;
    position: relative;
}

.container-slider {
  display: flex;
  flex-direction: column;
  justify-content: center;
  flex-direction: column;
  align-content: center;
  align-items: center;
  width:100%;
  height: 35vh;
  z-index: 9999;
}


.slider {
  -webkit-appearance: none;
  width: 20%;
  height: 1rem;
  background: transparent;
  border: #567C70 solid 1px;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

#slider {
    margin-top: 5rem;
    width: 90vw;
    object-fit: none;
    margin-bottom: -15rem;
    display: block;
}


.dateinfo {
    margin-bottom: 1rem;
}


.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 15px;
  height: 35px;
  background: #567C70;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 15px;
  height: 35px;
  background: #567C70;
  cursor: pointer;
}

.columns-bg {
  margin-top: 2rem;
  background-image:
    linear-gradient(
      to right, 
      #000000,
      #0b00ff,
      #7c0091,
      #00fe01,
      #fff400,
      #ff0000
    );
  height: 20px;
  width: 250px;
}

.test {
  display: flex;
  flex-direction: row;
  margin-top: 2rem;
  justify-content: space-between;
}

.image {
  display: flex;
  justify-content: center;
  align-items: center;
}


</style>
    <div class="slidecontainer">
      <div class="container-slider">
      <h2>No2 uitstoot Europa</h2>
      <p>Selecteer de landen die u wilt vergelijken</p>
      <p class='dateinfo'>Week: {currentImage}</p>
      <input type="range" class='slider' min='1' max='20' bind:value={currentImage} on:change={() => changeImage(currentImage)}>
      <div class="columns-bg">
        <div class="test">
        <p>Goed</p>
        <p>Middelmatig</p>
        <p>slecht</p>
      </div>
      </div>
    </div>
    <div class="image">
      <img id='slider' src='assets/slider/week1.png' alt='NO2 uitstoot'>
    </div>
      <Compare week={currentImage} />
      </div>




