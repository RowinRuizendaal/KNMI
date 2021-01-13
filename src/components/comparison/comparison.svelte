<script>
    import { onMount } from 'svelte';

    onMount(() => {
    const slider = document.querySelector('.slider input');
    const img = document.querySelector('.images .img-2')
    const dragLine = document.querySelector('.slider .drag-line')

    slider.oninput = () => {
        let sliderVal = slider.value;
        dragLine.style.left = sliderVal + '%';
        img.style.width = sliderVal + '%';
    }
    })
</script>
<style>
    h2 {
        text-align: center;
    }
    section {
        margin-top: 2rem;
    }
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .wrapper {
        position: relative;
        height: 500px;
        width: 750px;
        background: #FFF;
        border: 7px solid #fff;
    }

    .wrapper .images {
        height: 100%;
        width: 100%;
        display: flex;
    }

    .wrapper .images .img-1 {
        height: 100%;
        width: 100%;
        background: url('../assets/comparison/week4.png') no-repeat;
    }

    .wrapper .images .img-2 {
        position: absolute;
        height: 100%;
        width: 50%;
        background: url('../assets/comparison/week4.png') no-repeat;
    }

    .wrapper .slider {
        position: absolute;
        top: 0;
        width: 100%;
        z-index: 99;
    }

    .wrapper .slider input {
        height: 486px;
        width: 100%;
        outline: none;
        -webkit-appearance: none;
        -moz-appearance: none;
        background: none;
    }

    .slider input::-webkit-slider-thumb {
        height: 486px;
        width: 3px;
        background: none;
        -webkit-appearance: none;
        cursor: col-resize;
    }

    .slider input::-moz-range-thumb {
        height: 468px;
        width: 3px;
        /* background: #fff; */
        cursor: pointer;
        cursor: col-resize;
    }

    .slider .drag-line {
        width: 3px;
        height: 486px;
        position: absolute;
        background: #fff;
        left: 49.85%;
        pointer-events: none;
    }

    .slider .drag-line::before,
    .slider .drag-line::after {
        position: absolute;
        content: '';
        width: 100%;
        height: 222px;
        background: #fff;
    }

    .slider .drag-line::before {
        top: 0;
    }

    .slider .drag-line::after {
        bottom: 0;
    }

    .slider .drag-line span {
        height: 42px;
        width: 42px;
        border: 3px solid #fff;
        background-color: #567C70;
        position: absolute;
        top: 50%;
        left: 50%;
        border-radius: 50%;
        transform: translate(-50%, -50%);
    }

    .slider .drag-line span::before,
    .slider .drag-line span::after {
        position: absolute;
        content: '';
        top: 50%;
        border: 10px solid transparent;
        border-bottom-width: 0px;
        border-right-width: 0px;
        transform: translate(-50%, -50%) rotate(45deg);
    }

    .slider .drag-line span::before {
        left: 40%;
        border-left-color: #fff;
    }

    .slider .drag-line span::after {
        left: 60%;
        border-top-color: #fff;
    }

    .icons {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 12px;
    }
    .circle {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
        height: 60px;
        width: 60px;
        border-radius: 50%;
        background-color: #587d71;
        margin-bottom: 2rem;
    }

    .circle h2 {
        text-align: center;
        font-size: 1rem;
        color: #fff;
    }
</style>



<section class="compare">
    <h2>landen vergelijken</h2>
    <div class="container">
       <div class="wrapper">
          <div class="images">
             <div class="img-1"></div>
             <div class="img-2"></div>
          </div>
          <div class="slider">
             <div class="drag-line">
                <span></span>
             </div>
             <input type="range" min='0' max='100' value='50'>
          </div>
       </div>
    </div>
    <div class="icons">
       <div class="circle">
           <h2>Icoon</h2>
       </div>
       <div class="circle">
        <h2>Icoon</h2>
       </div>
       <div class="circle">
        <h2>Icoon</h2>
       </div>
       <div class="circle">
        <h2>Icoon</h2>
       </div>
    </div>
 </section>
 
 
