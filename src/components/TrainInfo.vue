<template>
  <div class="d-flex justify-space-around mb-6 ">
    <div id="trainTime" style="height: 500px;width: 500px;"></div>
 <!--   <div id="trainAuc" style="height: 500px;width: 500px;"></div>
    <div id="treeModel" style="height: 500px;width: 500px;"></div> -->
  </div>

</template>

<script>
  import * as echarts from "echarts";
  import axios from 'axios';
  export default{
    name: "TrainInfo",
    data(){
      return{
        trainTimeTimer: "",
        trainAucTimer: "",
        treeModelTimer: ""
      }
    },
    components: {},
    methods:{
      drawTrainTime() {
        axios.post("http://10.112.90.254:10000/show/trainTime").then(res=>{
          console.log(res.data);
          var chartDom = document.getElementById('trainTime');
          var myChart = echarts.init(chartDom);
          var option;
          var E2E_time_dto = res.data.E2E_time_dto;
          var mean_round_time_dto = res.data.mean_round_time_dto;
          var epoch_dto = res.data.epoch_dto;
          option = {
            title: {
              text: '训练时间信息'
            },
            tooltip: {
              trigger: 'axis'
            },
            legend: {
              data: ['当前训练时间', '平均每轮训练时间'],
              top:"6%"
            },
            grid: {
              left: '3%',
              right: '4%',
              bottom: '3%',
              containLabel: true
            },
            toolbox: {
              feature: {
                saveAsImage: {}
              }
            },
            xAxis: {
              type: 'category',
              boundaryGap: false,
              data: epoch_dto
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '当前训练时间',
                type: 'line',
                data: E2E_time_dto
              },
              {
                name: '平均每轮训练时间',
                type: 'line',
                data: mean_round_time_dto
              }
            ]
          };
          option && myChart.setOption(option);
        });
      },
      drawTrainAuc() {
        axios.post("http://10.112.90.254:10000/show/trainAuc").then(res=>{
          console.log(res.data);
          var chartDom = document.getElementById('trainAuc');
          var myChart = echarts.init(chartDom);
          var option;
          var E2E_time_dto = res.data.E2E_time_dto;
          var mean_round_time_dto = res.data.mean_round_time_dto;
          var epoch_dto = res.data.epoch_dto;
          option = {
            title: {
              text: '训练时间信息'
            },
            tooltip: {
              trigger: 'axis'
            },
            legend: {
              data: ['当前训练时间', '平均每轮训练时间'],
              top:"6%"
            },
            grid: {
              left: '3%',
              right: '4%',
              bottom: '3%',
              containLabel: true
            },
            toolbox: {
              feature: {
                saveAsImage: {}
              }
            },
            xAxis: {
              type: 'category',
              boundaryGap: false,
              data: epoch_dto
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '当前训练时间',
                type: 'line',
                stack: 'Total',
                data: E2E_time_dto
              },
              {
                name: '平均每轮训练时间',
                type: 'line',
                stack: 'Total',
                data: mean_round_time_dto
              }
            ]
          };
          option && myChart.setOption(option);
        });
      },
      drawTrainModel() {
      axios.post("http://10.112.90.254:10000/show/trainModel").then(res=>{
        console.log(res.data);
        var chartDom = document.getElementById('trainModel');
        var myChart = echarts.init(chartDom);
        var option;
        var E2E_time_dto = res.data.E2E_time_dto;
        var mean_round_time_dto = res.data.mean_round_time_dto;
        var epoch_dto = res.data.epoch_dto;
        option = {
          title: {
            text: '训练时间信息'
          },
          tooltip: {
            trigger: 'axis'
          },
          legend: {
            data: ['当前训练时间', '平均每轮训练时间'],
              top:"6%"
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: epoch_dto
          },
          yAxis: {
            type: 'value'
          },
          series: [
            {
              name: '当前训练时间',
              type: 'line',
              stack: 'Total',
              data: E2E_time_dto
            },
            {
              name: '平均每轮训练时间',
              type: 'line',
              stack: 'Total',
              data: mean_round_time_dto
            }
          ]
        };
        option && myChart.setOption(option);
      });
    },
    },
    mounted() {
      this.drawTrainTime();
      this.trainTimeTimer = setInterval(this.drawTrainTime, 30000);
    }
  }

</script>

<style>
</style>
