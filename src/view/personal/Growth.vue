<template>
    <div class="growthGraph">
      <div v-for="item in graphList" :id="item.id"></div>
    </div>
</template>
<script>
  let echarts = require('echarts/lib/echarts')
  require('echarts/lib/chart/line')
  require('echarts/lib/component/title')
  require('echarts/lib/component/tooltip')
  
  export default {
    data () {
      return {
        graphList: [{
          id: 'ability',
          title: '能力分值',
          data: [1, 5, 3],
          lineColor: 'orange'
        }, {
          id: 'credit',
          title: '信用分值',
          data: [6, 3, 4],
          lineColor: 'red'
        }, {
          id: 'skill',
          title: '技能分值',
          data: [3, 4, 5],
          lineColor: 'blue'
        }, {
          id: 'trade',
          title: '交易金额',
          data: [3, 2, 4],
          lineColor: 'pink'
        }],
        date: ['2017-05-11', '2017-06-11', '2017-07-11']
      }
    },
    components: {},
    methods: {
      setOptions (title, lineColor, data) {
        let options = {
          title: {
            text: title,
            textStyle: {
              color: 'grey',
              fontSize: 18
            }
          },
          tooltip: {
            trigger: 'axis'
          },
          toolbox: {
            show: false
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: this.date,
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              textStyle: {
                color: '#ccc'
              }
            }
          },
          yAxis: {
            type: 'value',
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              textStyle: {
                color: '#ccc'
              }
            },
            splitLine: {
              lineStyle: {
                color: '#eee'
              }
            }
          },
          series: [{
            type: 'line',
            data: data,
            symbol: 'none',
            itemStyle: {
              normal: {
                lineStyle: {
                  color: lineColor
                }
              }
            }
          }]
        }
        return options
      }
    },
    computed: {},
    mounted () {
      for (var value of this.graphList) {
        // alert(value)
        let echart = echarts.init(document.getElementById(value.id))
        let options = this.setOptions(value.title, value.lineColor, value.data)
        echart.setOption(options)
      }
    }
  }
</script>
<style scoped lang="scss" rel="stylesheet/scss">
  .growthGraph{
    display: flex;
    display: -webkit-flex;
    flex-wrap: wrap;
    justify-content: space-between;
    div{
      width: 40%;
      height: 250px;
      margin: 3em;
      box-shadow: 0 0 10px #eee;
      padding: 1em;
    }
  }

</style>
