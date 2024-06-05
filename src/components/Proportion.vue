<template>
  <div class="d-flex justify-space-around mb-6 ">
    <div id="proportion" style="height: 500px;width: 500px;"></div>
  </div>

</template>

<script>
  import * as echarts from "echarts";
  import axios from 'axios';
  export default{
    name: "Proportion",
    data(){
      return{
        proportionTimer: "",
      }
    },
    components: {},
    methods:{
      drawProportion() {
        axios.post("http://10.112.90.254:10000/show/proportion").then(res=>{
          console.log(res.data);
          var chartDom = document.getElementById('proportion');
          var myChart = echarts.init(chartDom);
          var option;
          var E2E_time = res.data.E2E_time;
          var total_transaction_latency = res.data.total_transaction_latency;
          var train_time = E2E_time - total_transaction_latency;
          console.log(train_time);
          option = {
            title: {
              text: '各项耗时占比',
              left: 'center'
            },
            tooltip: {
              trigger: 'item'
            },
            toolbox: {
              feature: {
                saveAsImage: {}
              }
            },
            legend: {
              orient: 'vertical',
              left: 'left'
            },
            series: [
              {
                name: '耗时',
                type: 'pie',
                radius: '50%',
                data: [
                  { value: train_time, name: '训练耗时' },
                  { value: total_transaction_latency, name: '事务耗时' }
                ],
                emphasis: {
                  itemStyle: {
                    shadowBlur: 10,
                    shadowOffsetX: 0,
                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                  }
                }
              }
            ]
          };
          option && myChart.setOption(option);
        });
      }
    },
    mounted() {
      this.drawProportion();
      this.transactionLatencyTimer = setInterval(this.drawProportion, 30000);
    },

  }

</script>

<style>
</style>
