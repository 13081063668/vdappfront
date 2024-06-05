<template>
  <v-card>
    <v-tabs
      v-model="tab"
      bg-color="primary"
    >
      <v-tab value="训练时间">训练信息</v-tab> <!--1.  平均每轮训练时间,总训练时间, 2. 模型精度auc, 3. 节点模型[树] -->
      <v-tab value="事务消耗">事务消耗</v-tab> <!-- 4. 平均事务延迟,总事务延迟, 5. 平均消耗gas,总gas, 6. 智能合约调用次数 -->
      <v-tab value="占比">占比</v-tab><!-- 7. 模型训练和事务消耗时间占比 -->

    </v-tabs>

    <v-card-text>
      <v-tabs-window v-model="tab">
        <v-tabs-window-item value="训练时间">
          <TrainInfo></TrainInfo>
        </v-tabs-window-item>

        <v-tabs-window-item value="事务消耗">
          <TransactionInfo></TransactionInfo>
        </v-tabs-window-item>

        <v-tabs-window-item value="占比">
          <Proportion></Proportion>
        </v-tabs-window-item>
      </v-tabs-window>
    </v-card-text>
  </v-card>
</template>
<script>
  export default {
    data: () => ({
      tab: null,
    }),
  }
</script>
<script setup>
  import TrainInfo from './TrainInfo.vue'
  import TransactionInfo from './TransactionInfo.vue'
  import Proportion from './Proportion.vue'

</script>

<style>
</style>
