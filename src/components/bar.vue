<template>
    <div id="app">
      <p class="tag">X轴行标签(List列表)<el-input v-model="xAxisLabels" class="empty"></el-input></p>
      <p class="tag">Y轴列标签(List列表)<el-input v-model="yAxisLabels" class="empty" placeholder="Type:Value" onlyread></el-input></p>
      <p class="tag">Data数据(List列表)<el-input v-model="dataValues" class="empty"></el-input></p>
      <p class="tag">提示信息<el-switch style="margin-left: 10px;" v-model="tooltips" /></p>
      <el-button @click="sendOptions" class="run">运行</el-button>
      <pre>{{ option }}</pre>
    </div>
  </template>
  
  <style scoped>
  .run {
    margin-left: 45%;
  }
  .tag {
    padding: 10px;
  }
  .empty {
    margin: 10px;
    width: 200px;
  }
  </style>
  
  <style>
  #app > div > div.left > div.bottom > button {
    margin-left: 45%;
  }
  </style>
  
  <script>
  export default {
    data() {
      return {
        xAxisLabels: '', // X轴标签的输入
        yAxisLabels: '', // Y轴标签的输入
        dataValues: '', // 数据值的输入
        option: "", // 图表配置对象
        tooltips: false
      };
    },
    methods: {
      generateOption() {
        const xAxisData = this.xAxisLabels.split(','); // 将X轴标签拆分为数组
        const data = this.dataValues.split(',').map(Number); // 将数据值拆分为数组并转换为数字类型
  
        this.option = {
          xAxis: {
            type: 'category',
            data: xAxisData
          },
          yAxis: {}, // 去除type属性
          series: [
            {
              data: data,
              type: 'bar'
            }
          ]
        };
  
        console.log("生成的Option对象:", this.option);
      },
      sendOptions(){
        this.generateOption();
        this.$emit('listen', this.option);
      }
    }
  };
  </script>
  