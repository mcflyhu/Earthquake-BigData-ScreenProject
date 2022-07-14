<template>
  <div>
    <Echart id="centreLeft2Chart" ref="centreLeft2ChartRef" :options="options" height="610px" width="810px"></Echart>
  </div>
</template>

<script>
import Echart from '@/common/echart';
export default {
  data() {
    return {
      options: {},
    };
  },
  components: {
    Echart,
  },
  props: {
    cdata: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    cdata: {
      handler(newData) {
        // 设置点的位置(经纬度)
        const geoCoordMap = {
          '上海': [121.480237, 31.236305, 20],
          '新疆': [87.623314, 43.832806, 20],
          '甘肃': [103.840692, 36.067312, 20],
          '北京': [116.413554, 39.911013, 20],
          '江苏': [118.802891, 32.064735, 20],
          '安徽': [117.235447, 31.82687, 20],
          '黑龙江': [126.542417, 45.807782, 20],
          '内蒙': [111.758518, 40.847461, 20],
          天津: [117.205914, 39.090908, 20],
          广东: [113.270793, 23.135308, 20],
          四川: [104.071216, 30.576279, 20],
          西藏: [91.121025, 29.650088, 20],
          浙江: [120.161693, 30.280059, 20],
          云南: [102.839667, 24.885953, 20],
          湖北: [114.311831, 30.598428, 20],
          辽宁: [123.438973, 41.811339, 20],
          山东: [117.001319, 36.671627, 20],
          海南: [110.206424, 20.050057, 20],
          河北: [114.520828, 38.048684, 20],
          陕西: [108.946306, 34.347436, 20],
          贵州: [106.636816, 26.652747, 20],
          重庆: [106.557165, 29.570997, 20],
          吉林: [125.33017, 43.82178, 20],
          湖南: [112.945333, 28.233971, 20],
          河南: [113.631349, 34.753488, 20],
          山西: [112.33, 37.54, 20],
          宁夏: [106.3586, 38.1775, 20],
          青海: [101.4038, 36.8207, 20],
          福建: [119.4543, 25.9222, 20],
          江西: [116.0046, 28.6633, 20],
          广西: [108.479, 23.1152, 20],
        };
        let seriesData = [
          {
            name: '上海',
          },
          {
            name: '新疆',
          },
          {
            name: '甘肃',
          },
          {
            name: '北京',
          },
          {
            name: '江苏',
          },
          {
            name: '安徽',
          },
          {
            name: '黑龙江',
          },
          {
            name: '内蒙',
          },
          {
            name: '天津',
          },
          {
            name: '广东',
          },
          {
            name: '四川',
          },
          {
            name: '西藏',
          },
          {
            name: '浙江',
          },
          {
            name: '云南',
          },
          {
            name: '湖北',
          },
          {
            name: '辽宁',
          },
          {
            name: '山东',
          },
          {
            name: '海南',
          },
          {
            name: '河北',
          },
          {
            name: '陕西',
          },
          {
            name: '贵州',
          },
          {
            name: '重庆',
          },
          {
            name: '吉林',
          },
          {
            name: '湖南',
          },
          {
            name: '河南',
          },
          {
            name: '山西',
          },
          {
            name: '宁夏',
          },
          {
            name: '青海',
          },
          {
            name: '福建',
          },
          {
            name: '江西',
          },
          {
            name: '广西',
          },
        ];
        let convertData = function (data) {
          let scatterData = [];
          for (var i = 0; i < data.length; i++) {
            var geoCoord = geoCoordMap[data[i].name];
            if (geoCoord) {
              scatterData.push({
                name: data[i].name,
                value: geoCoord.concat(data[i].value),
              });
            }
          }
          return scatterData;
        };
        this.options = {
          showLegendSymbol: true,
          tooltip: {
            trigger: 'item',
            textStyle: {
              fontSize: 14,
              lineHeight: 22,
            },
            position: point => {
              // 固定在顶部
              return [point[0] + 50, point[1] - 20];
            },
            // 如果需要自定义 tooltip样式，需要使用formatter
            /*
              formatter: params => {
                return `<div style=""> ... </div>`
              }
            */
          },
          visualMap: {
            min: 0,
            max: 10,
            show: false,
            seriesIndex: 0,
            // 颜色
            inRange: {
              color: ['rgba(41,166,206, .5)', 'rgba(69,117,245, .9)'],
            },
          },
          // 底部背景
          geo: {
            show: true,
            aspectScale: 0.85, //长宽比
            zoom: 1.2,
            top: '10%',
            left: '10%',
            map: 'china',
            roam: false,
            itemStyle: {
              normal: {
                areaColor: 'rgba(0,0,0,0)',
                shadowColor: 'rgba(7,114,204, .8)',
                shadowOffsetX: 5,
                shadowOffsetY: 5,
              },
              emphasis: {
                areaColor: '#00aeef',
              },
            },
          },
          series: [
            {
              name: '相关指数',
              type: 'map',
              aspectScale: 0.85, //长宽比
              zoom: 1.2,
              mapType: 'china', // 自定义扩展图表类型
              top: '10%',
              left: '10%',
              itemStyle: {
                normal: {
                  color: 'red',
                  areaColor: 'rgba(19,54,162, .5)',
                  borderColor: 'rgba(0,242,252,.3)',
                  borderWidth: 1,
                  shadowBlur: 7,
                  shadowColor: '#00f2fc',
                },
                emphasis: {
                  areaColor: '#4f7fff',
                  borderColor: 'rgba(0,242,252,.6)',
                  borderWidth: 2,
                  shadowBlur: 10,
                  shadowColor: '#00f2fc',
                },
              },
              label: {
                formatter: params => `${params.name}`,
                show: true,
                position: 'insideRight',
                textStyle: {
                  fontSize: 14,
                  color: '#efefef',
                },
                emphasis: {
                  textStyle: {
                    color: '#fff',
                  },
                },
              },
              data: newData,
            },
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              symbolSize: 7,
              effectType: 'ripple',
              legendHoverLink: false,
              showEffectOn: 'render',
              rippleEffect: {
                period: 4,
                scale: 2.5,
                brushType: 'stroke',
              },
              zlevel: 1,
              itemStyle: {
                normal: {
                  color: '#99FBFE',
                  shadowBlur: 5,
                  shadowColor: '#fff',
                },
              },
              data: convertData(seriesData),
            },
          ],
        };
        // 重新选择区域
        this.handleMapRandomSelect();
      },
      immediate: true,
      deep: true,
    },
  },
  methods: {
    // 开启定时器
    startInterval() {
      const _self = this;
      // 应通过接口获取配置时间，暂时写死5s
      const time = 2000;
      if (this.intervalId !== null) {
        clearInterval(this.intervalId);
      }
      this.intervalId = setInterval(() => {
        _self.reSelectMapRandomArea();
      }, time);
    },
    // 重新随机选中地图区域
    reSelectMapRandomArea() {
      const length = 9;
      this.$nextTick(() => {
        try {
          const map = this.$refs.centreLeft2ChartRef.chart;
          let index = Math.floor(Math.random() * length);
          while (index === this.preSelectMapIndex || index >= length) {
            index = Math.floor(Math.random() * length);
          }
          map.dispatchAction({
            type: 'mapUnSelect',
            seriesIndex: 0,
            dataIndex: this.preSelectMapIndex,
          });
          map.dispatchAction({
            type: 'showTip',
            seriesIndex: 0,
            dataIndex: index,
          });
          map.dispatchAction({
            type: 'mapSelect',
            seriesIndex: 0,
            dataIndex: index,
          });
          this.preSelectMapIndex = index;
        } catch (error) {
          console.log(error)
        }
      });
    },
    handleMapRandomSelect() {
      this.$nextTick(() => {
        try {
          const map = this.$refs.centreLeft2ChartRef.chart;
          const _self = this;
          setTimeout(() => {
            _self.reSelectMapRandomArea();
          }, 0);
          // 移入区域，清除定时器、取消之前选中并选中当前
          map.on('mouseover', function (params) {
            clearInterval(_self.intervalId);
            map.dispatchAction({
              type: 'mapUnSelect',
              seriesIndex: 0,
              dataIndex: _self.preSelectMapIndex,
            });
            map.dispatchAction({
              type: 'mapSelect',
              seriesIndex: 0,
              dataIndex: params.dataIndex,
            });
            _self.preSelectMapIndex = params.dataIndex;
          });
          // 移出区域重新随机选中地图区域，并开启定时器
          map.on('globalout', function () {
            _self.reSelectMapRandomArea();
            _self.startInterval();
          });
          this.startInterval();
        } catch (error) {
          console.log(error)
        }
      });
    },
  },
};
</script>
