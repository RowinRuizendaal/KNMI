<script>
import Chart from 'chart.js'
import {
    onMount
} from 'svelte';


export let getal


onMount(async () => {
    const data = await fetch('./dataset/Netherlands.json').then(res => res.json());
    const data2 = await fetch('./dataset/Italy.json').then(res => res.json());



    const convertDate = (date) => {
        return date = data.map(d => d.date.value)
            .filter(d => new Date(d).getFullYear() === 2020)
            .map(d => `${new Date(d).getDate()} / ${new Date(d).getMonth()} / ${new Date(d).getFullYear()}`)
    }


    const test = (data) => {
        const aap = []
        data.map((d) => {
            aap.push(d.number)
        })
        return aap
    }



    const ctx = document.getElementById('myChart').getContext('2d');
    const ctx2 = document.getElementById('myChart2').getContext('2d');

    new Chart(ctx, {
        type: 'line',
        data: {
            labels: convertDate(data),
            datasets: [{
                label: 'Nederland',
                backgroundColor: 'rgb(255,227,80)',
                borderColor: 'rgb(255,227,80)',
                data: test(data),
                fill: false
            }, ]

        }
    })
    new Chart(ctx2, {
        type: 'line',
        data: {
            labels: convertDate(data2),
            datasets: [{
                label: 'Italie',
                backgroundColor: 'rgb(255, 99, 132)',
                borderColor: 'rgb(255, 99, 132)',
                data: test(data2),
                fill: false
            }, ]

        }
    })
})
    
</script>
    
    <style>
    
        .chart-container {
            position: relative;
            height: 5vh;
            width: 40vw
        }
    
        @media only screen and (max-width: 600px) {
        .chart-container {
            height: 100vh;
            width: 100%;
        }
      }
    </style>
    
    
    
    <div class="chart-container">
    <canvas id="myChart"></canvas>
    <canvas id="myChart2"></canvas>
    {getal}
    </div>