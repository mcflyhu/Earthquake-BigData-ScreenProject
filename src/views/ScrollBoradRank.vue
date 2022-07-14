
<template>
    <div id="ScrollBoardRank">
        <div class="bg-color-black">
            <div class="d-flex pt-2 pl-2">
                <span>
                    <icon name="chart-line" class="text-icon"></icon>
                </span>
                <div class="d-flex">
                    <span class="fs-xl text mx-2">各省重大地震次数</span>
                </div>
            </div>
            <div class="d-flex jc-center body-box">
                <dv-scroll-ranking-board class="dv-scr-rank-board" :config="config" />
            </div>
        </div>
    </div>
</template>
<script>
import { csvParse } from 'd3-dsv';
export default {
    data() {
        return {
            config: {
                data: [],
                rowNum: 2,
                carousel: 'page'
            }
        };
    },
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
                    //console.log(this.config.data);
                    //console.log(csv);
                });
        }
    }
}
</script>

<style lang="scss" scoped>
$box-height: 200px;
$box-width: 500px;

#ScrollBoardRank {
    padding: 16px;
    padding-top: 20px;
    height: $box-height;
    width: $box-width;
    border-radius: 5px;

    .bg-color-black {
        height: $box-height - 30px;
        border-radius: 10px;
    }

    .text {
        color: #c3cbde;
    }

    .body-box {
        border-radius: 10px;
        overflow: hidden;

        .dv-scr-rank-board {
            height: 160px;
        }
    }
}
</style>