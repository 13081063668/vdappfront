<template>
  <div class="d-flex justify-space-around mb-6 ">
    <div id="transactionLatency" style="height: 500px;width: 500px;"></div>
    <div id="transactionCost" style="height: 500px;width: 500px;"></div>
  </div>

</template>

<script>
  import * as echarts from "echarts";
  import axios from 'axios';
  export default{
    name: "TransactionInfo",
    data(){
      return{
        transactionLatencyTimer: "",
        transactionCostTimer: "",
        transactionTimesTimer: ""
      }
    },
    components: {},
    methods:{
      drawTransactionLatency() {
        axios.post("http://10.112.90.254:10000/show/transactionLatency").then(res=>{
          console.log(res.data);
          var chartDom = document.getElementById('transactionLatency');
          var myChart = echarts.init(chartDom);
          var option;
          var total_transaction_latency_dto = res.data.total_transaction_latency_dto;
          var mean_transaction_latency_dto = res.data.mean_transaction_latency_dto;
          var epoch_dto = res.data.epoch_dto;
          var total_call_times_dto = res.data.total_call_times_dto;
          option = {
            title: {
              text: '事务延迟信息'
            },
            tooltip: {
              trigger: 'axis'
            },
            legend: {
              data: ['当前事务总延迟', '平均事务延迟'],
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
              data: total_call_times_dto
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '当前事务总延迟',
                type: 'line',
                data: total_transaction_latency_dto
              },
              {
                name: '平均事务延迟',
                type: 'line',
                data: mean_transaction_latency_dto
              }
            ]
          };
          option && myChart.setOption(option);
        });
      },
      drawTransactionCost() {
        axios.post("http://10.112.90.254:10000/show/transactionCost").then(res=>{
          console.log(res.data);
          var chartDom = document.getElementById('transactionCost');
          var myChart = echarts.init(chartDom);
          var option;
          var total_transaction_cost_dto = res.data.total_transaction_cost_dto;
          var mean_transaction_cost_dto = res.data.mean_transaction_cost_dto;
          var total_call_times_dto = res.data.total_call_times_dto;
          var epoch_dto = res.data.epoch_dto;
          option = {
            title: {
              text: '训练gas消耗'
            },
            tooltip: {
              trigger: 'axis'
            },
            legend: {
              data: ['当前总事务消耗', '平均每轮事务消耗'],
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
              data: total_call_times_dto
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '当前总事务消耗',
                type: 'line',
                data: total_transaction_cost_dto
              },
              {
                name: '平均每轮事务消耗',
                type: 'line',
                data: mean_transaction_cost_dto
              }
            ]
          };
          option && myChart.setOption(option);
        });
      },
    },
    mounted() {
      this.drawTransactionLatency();
      this.transactionLatencyTimer = setInterval(this.drawTransactionLatency, 30000);
      this.drawTransactionCost();
      this.transactionLatencyTimer = setInterval(this.drawTransactionCost, 30000);

    },

  }

</script>

<style>
</style>
