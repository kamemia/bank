<script>
    import { Chart } from 'flowbite-svelte';

  
    const options = {
      series: [52.8, 26.8, 20.4],
      colors: ['#1C64F2', '#16BDCA', '#9061F9'],
      chart: {
        height: 320,
        width: '100%',
        type: 'pie'
      },
      stroke: {
        colors: ['white'],
        lineCap: ''
      },
      plotOptions: {
        pie: {
          labels: {
            show: true
          },
          size: '50%',
          dataLabels: {
            offset: -25
          }
        }
      },
      labels: ['Direct', 'Organic search', 'Referrals'],
      dataLabels: {
        enabled: true,
        style: {
          fontFamily: 'Inter, sans-serif'
        }
      },
      legend: {
        position: 'bottom',
        fontFamily: 'Inter, sans-serif'
      },
      yaxis: {
        labels: {
          formatter: function (value) {
            return value + '%';
          }
        }
      },
      xaxis: {
        labels: {
          formatter: function (value) {
            return value + '%';
          }
        },
        axisTicks: {
          show: false
        },
        axisBorder: {
          show: false
        }
      }
    };
  </script>
  

   
  
<Chart {options} class="py-6" />
  
    

