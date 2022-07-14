<template>
    <div>
        <Echart :options="options" id="bottomChart" height="320px" width="100%"></Echart>
    </div>
</template>

<script>
import Echart from '@/common/echart'
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
            type: Object,
            default: () => ({})
        },
    },
    watch: {
        cdata: {
            handler(newData) {
                this.options = {
                    // 这里编写 ECharts 配置
                    xAxis: {
                        type: 'value',
                        scale: true
                    },
                    yAxis: {
                        type: 'value',
                        scale: true
                    },
                    series: [
                        {
                            type: 'effectScatter',
                            symbolSize: 20,
                            data: [
                                [8, 589.2],
                                [3.2, 103]
                            ]
                        },
                        {
                            data: newData.data,
                            type: 'scatter',
                            symbolSize: 5,
                            itemStyle: {
                                borderColor: '#555'
                            },
                        }
                    ]
                }
            },
            // 立即监听
            immediate: true,
            // 深度监听
            deep: true
        }
    }
}
</script>