 <template>
    <div id="centerLeft">
        <div class="up">
            <div class="bg-color-black">
                <div class="d-flex pt-2 pl-2">
                    <span>
                        <icon name="chart-line" class="text-icon"></icon>
                    </span>
                    <div class="d-flex">
                        <span class="fs-xl text mx-2">全球震源深度排行</span>
                    </div>
                </div>
                <div class="d-flex jc-center body-box">
                    <dv-scroll-board class="dv-scr-board" :config="rank" />
                </div>
            </div>
        </div>
        <div class="down">
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
                    <dv-scroll-ranking-board class="dv-scr-rank-board" :config="count" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { csvParse } from 'd3-dsv';
export default {
    data() {
        return {
            count: {
                data: [],
                rowNum: 2,
                carousel: "page"
            },
            rank: {
                header: ['时间', '地区', '震源深度'],
                data: [],
                rowNum: 5, //表格行数
                headerHeight: 35,
                headerBGC: '#0f1325', //表头
                oddRowBGC: '#473C8B', //奇数行
                evenRowBGC: '#EE799F', //偶数行
                index: true,
                columnWidth: [50, 140, 200, 80],
                align: ['center', 'center', 'center', 'center']
            }
        };
    },
    created() {
        this.getRankData();
        this.getCountData();
    },
    methods: {
        getCountData() {
            this.$axios
                .get("/地区次数.csv")
                .then(res => {
                    var csv = csvParse(res.data, (d) => {
                        return {
                            name: d.area,
                            value: +d.count
                        };
                    });
                    this.count.data = csv;
                    this.count = { ...this.count };
                    //console.log(this.count.data);
                    //console.log(csv);
                });
        },
        getRankData() {
            this.$axios
                .get("/Top500Magnitude.csv")
                .then(res => {
                    var csv = csvParse(res.data, (d) => {
                        return {
                            time: d.time,
                            area: d.place,
                            magnitude: d.zhenji
                        };
                    });
                    var obj = csv;
                    var arr = [];
                    for (var i in obj) {
                        var item = [];
                        item = Object.values(obj[i]);
                        arr.push(item);
                    }

                    this.rank.data = arr;
                    this.rank = { ...this.rank };
                    //console.log(this.rank.data);
                    //console.log(csv);
                });
        }
    },
}
</script>

<style lang="scss" scoped>
$box-height: 610px;
$box-width: 500px;

#centerLeft {
    display: flex;
    flex-direction: column;

    padding: 16px;
    padding-top: 20px;
    height: $box-height;
    width: $box-width;
    border-radius: 5px;

    .bg-color-black {
        border-radius: 10px;
    }

    .up {
        display: flex;

        .text {
            color: #c3cbde;
        }

        .body-box {
            border-radius: 10px;
            overflow: hidden;

            .dv-scr-board {
                width: 460px;
                height: 340px;
            }
        }

    }

    .down {
        display: flex;
        padding-top: 10px;
        width: $box-width;

        .text {
            color: #c3cbde;
        }

        .body-box {
            border-radius: 10px;
            overflow: hidden;

            .dv-scr-rank-board {
                width: 460px;
                height: 160px;
            }
        }
    }

}
</style>