<template>
    <div class="container">
      <div class="left">
        <div class="top">
          <el-popover placement="bottom" :width="500" trigger="click">
            <template #reference>
              <el-button id="popover">点我选择图例</el-button>
            </template>
            <h4>#基础图形</h4>
            <el-button @click="routerto('bar')">柱状图</el-button>
            <el-button @click="routerto('line')">折线图</el-button>
            <el-divider />
            <el-button>其他图表类型</el-button>
          </el-popover>
        </div>
        <div class="bottom">
          <router-view @listen="updateOptions"></router-view>
        </div>
      </div>
      <div class="right">
        <div ref="echartsContainer" class="echarts-container"></div>
      </div>
    </div>
  </template>
  
  <script>
  import { ElPopover, ElButton, ElDivider } from 'element-plus';
  import * as echarts from 'echarts';
  
  export default {
    components: {
      ElPopover,
      ElButton,
      ElDivider
    },
    data() {
      return {
        options: {}
      };
    },
    mounted() {
      this.initEcharts();
    },
    methods: {
      routerto(pageName) {
        this.$router.push({ name: pageName });
      },
      updateOptions(option) {
        this.options = option;
        this.updateEcharts();
      },
      initEcharts() {
        this.echartsInstance = echarts.init(this.$refs.echartsContainer);
        this.updateEcharts();
      },
      updateEcharts() {
        // 使用 options 更新 Echarts 实例
        if (this.echartsInstance && this.options) {
          this.echartsInstance.setOption(this.options);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .container {
    display: flex;
    height: 100vh;
  }
  
  .left, .right {
    flex: 1;
  }
  
  .left {
    display: flex;
    flex-direction: column;
    background-color: white;
  }
  
  .top {
    flex: 0 1 auto;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    padding: 0px;
  }
  
  .bottom {
    flex: 1;
    margin-top: 10px;
    background-color: white;
  }
  
  .right {
    background-color: #f0f0f0;
  }
  
  #popover {
    margin-top: 10px;
  }
  
  .echarts-container {
    width: 100%;
    height: 100%;
  }
  </style>
  