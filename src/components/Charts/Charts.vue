<template>
    <div>
        <apexchart :options="chartOptions" :series="chartData" type="line" height="350" />
    </div>
</template>
  
<script>
import VueApexCharts from 'vue3-apexcharts';

export default {
    name: 'charsJS',
    components: {
        apexchart: VueApexCharts,
    },
    props: {
        chartData: Array, // Define chartData as a prop
    },
    data() {
        return {
            chartOptions: {
                chart: {
                    type: 'line',
                    height: 350,
                },
                xaxis: {
                    type: 'datetime',
                },
                title: {
                    text: 'Bitcoin Price Per Minute',
                    align: 'left',
                },
            },
        };
    },
};
</script>
  