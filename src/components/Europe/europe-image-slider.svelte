<script>
    const changeImage = (count) => {
    let src = `assets/slider/week${count}.png`
    document.getElementById('slider').src = src
    }

    let currentImage = 1
</script>

<style>
.slidecontainer {
    margin-top: 4rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.slider {
  -webkit-appearance: none;
  width: 20%;
  height: 1rem;
  background: transparent;
  border: #00689A solid 1px;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

#slider {
    margin-top: 2rem;
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
  background: #00689A;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 15px;
  height: 35px;
  background: #00689A;
  cursor: pointer;
}
</style>

    <div class="slidecontainer">
        <p class='dateinfo'>Week: {currentImage}</p>
        <input type="range" class='slider' min='1' max='4' bind:value={currentImage} on:change={() => changeImage(currentImage)}>
        <img id='slider' src='assets/slider/week1.png' alt='NO2 uitstoot'>
      </div>




