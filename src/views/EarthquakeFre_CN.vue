<template>
    <div id="Earthquake_CN">
        <div class="bg-color-black">
            <div class="d-flex pt-2 pl-2">
                <span>
                    <!-- <icon name="chart-pie" class="text-icon"></icon>-->
                </span>
                <div class="d-flex">
                    <span class="fs-xl text mx-2">地图数据</span>
                    <dv-decoration-1 class="dv-dec-1" />
                </div>
            </div>
            <div class="d-flex jc-center">
                <CenterLeft2Chart />
            </div>
        </div>
    </div>
</template>

<script>
import CenterLeft2Chart from '../components/echart/centerLeft/centerLeft2Chart';

export default {
    data() {
        return {};
    },
    components: { CenterLeft2Chart },
    /*
    created() {
        this.getData();
    },
    methods: {
        getData() {
            this.$axios
                .get("/地区次数.csv")
                .then(res => {
                    var csv = csvParse(res.data, (d) => {
                        return {
                            name: d.area,
                            value: +d.count
                        };
                    });
                    this.config.data = csv;
                    this.config = { ...this.config };
                    console.log(this.config.data);
                    //console.log(csv);
                });
        }
    }
    */
}

</script>

<style lang="scss" scoped>
#Earthquake_CN {
    $box-width: 810px;
    $box-height: 610px;
    padding: 16px;
    height: $box-height;
    min-width: $box-width;
    border-radius: 5px;

    .bg-color-black {
        height: $box-height - 30px;
        border-radius: 10px;
    }

    .text {
        color: #c3cbde;
        font-size: larger;
    }

    .dv-dec-1 {
        position: relative;
        width: 100px;
        height: 20px;
        top: -3px;
    }

    .chart-box {
        margin-top: 16px;
        width: 170px;
        height: 170px;

        .active-ring-name {
            padding-top: 10px;
        }
    }
}
</style>
