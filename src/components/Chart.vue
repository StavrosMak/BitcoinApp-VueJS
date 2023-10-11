<template>
    <div>
        <apexchart :options="chartOptions" :series="chartData" type="area" height="350" />
    </div>
</template>
  
 
<script>
import VueApexCharts from 'vue3-apexcharts';

export default {
    name: 'ChartJS',
    components: {
        apexchart: VueApexCharts,
    },
    data() {
        return {
            chartOptions: {
                chart: {
                    type: 'area',
                    height: 350,
                    zoom: {
                        enabled: false,
                    },
                },
                dataLabels: {
                    enabled: false,
                },
                stroke: {
                    curve: 'straight',
                },
                title: {
                    text: 'Fundamental Analysis of Stocks',
                    align: 'left',
                },
                subtitle: {
                    text: 'Price Movements',
                    align: 'left',
                },
                xaxis: {
                    type: 'datetime',
                },
                yaxis: {
                    opposite: true,
                },
                legend: {
                    horizontalAlign: 'left',
                },
            },
            chartData: [
                {
                    name: "STOCK ABC",
                    data: [
                        [new Date('2023-10-01').getTime(), 30],
                        [new Date('2023-10-02').getTime(), 40],
                        // ... your data points here ...
                    ],
                },
            ],
        };
    },
};
</script>

  