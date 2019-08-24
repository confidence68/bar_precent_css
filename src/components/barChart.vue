<template>
  <div class="linechartWrap">
    <v-chart class="barchart" :options="options" autoresize />
  </div>
</template>

<script>
import ECharts from 'vue-echarts'
import 'echarts/lib/chart/bar'
import 'echarts/lib/component/tooltip'
import 'echarts/lib/component/title'
import 'echarts/lib/component/toolbox'

export default {
  components: {
    'v-chart': ECharts
  },
  props: {
    barData: {
      type: Object,
      default() {
        return {
          data: [11, 33, 77],
          title: ['07-01', '07-02', '07-03']

        }
      }
    }
  },
  computed: {
    options() {
      return {
        grid: {
          show: 'true',
          borderWidth: '0',
          height: '72%',
          width: '90%',
          x: '12%',
          y: '20%'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'none'
          },
          formatter: '{b0}: {c0}%'
        /* formatter: function(params) {
            var result = '';
            params.forEach(function (item) {
                result += item.marker + " " + item.seriesName + " : " + item.value +"</br>";
            });
            return result;
        }*/
        },
        backgroundColor: '#fff', // 背景色
        yAxis: {
          show: false, // 是否显示x轴
          type: 'value'
        },
        xAxis: {
          type: 'category',
          axisLabel: {
            show: true,
            textStyle: {
              color: '#666' // y轴字体颜色
            }
          },
          splitLine: { show: false }, // 横向的线
          axisTick: { show: false }, // y轴的端点
          axisLine: { show: false }, // y轴的线
          data: this.barData.title
        },
        series: [
          {
            type: 'bar',
            itemStyle: {
              normal: {
                barBorderRadius: 25,
                color: '#3990FF'
              }
            },
            barWidth: 25,
            data: this.barData.data
          },
          {
            name: '外框',
            type: 'bar',
            itemStyle: {
              normal: {
                barBorderRadius: 25,
                color: '#e5e5e5' // rgba设置透明度0.14
              }
            },
            barGap: '-100%',
            z: 0,
            barWidth: 25,
            data: [100, 100, 100]
          }
        ]
      }
    }
  }

}
</script>

<style lang="scss" scoped>
.linechartWrap{width:100%;}
.barchart{height:243px;width:100%;}

</style>
