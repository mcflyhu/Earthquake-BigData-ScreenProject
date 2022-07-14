<template>
    <div>
        <!-- 各省份发生重大地震次数 -->
        <Echart :options="options" id="bottomLeftChart" height="320px" width="100%"></Echart>
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
                    tooltip: {
                        trigger: "axis",
                        backgroundColor: "rgba(255,255,255,0.1)",
                        axisPointer: {
                            type: "shadow",
                            label: {
                                show: true,
                                backgroundColor: "#7B7DDC"
                            }
                        }
                    },
                    grid: {
                        x: "8%",
                        width: "88%",
                        y: "4%"
                    },
                    xAxis: {
                        data: newData.area,
                        axisLine: {
                            lineStyle: {
                                color: "#B4B4B4"
                            }
                        },
                        axisTick: {
                            show: false
                        }
                    },
                    yAxis: [
                        {
                            axisLine: {
                                lineStyle: {
                                    color: "#B4B4B4"
                                }
                            },

                            axisLabel: {
                                formatter: "{value} "
                            }
                        }
                    ],
                    series: [
                        {
                            name: "地区",
                            type: "bar",
                            barWidth: 10,
                            itemStyle: {
                                normal: {
                                    barBorderRadius: 5,
                                    color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        { offset: 0, color: "#956FD4" },
                                        { offset: 1, color: "#3EACE5" }
                                    ])
                                }
                            },
                            data: newData.count
                        },
                    ]
                }
            },
            immediate: true,
            deep: true
        },
    },
}
</script>