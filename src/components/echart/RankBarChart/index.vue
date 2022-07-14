<template>
    <div>
        <Chart :cdata="cdata" />
    </div>
</template>

<script>
import Chart from './chart.vue'
import { csvParse } from 'd3-dsv'
export default {
    data() {
        return {
            cdata: {
                area: [],
                count: []
            }
        }
    },
    components: {
        Chart,
    },
    mounted() {
        this.setData();
    },
    methods: {
        // 根据自己的业务情况修改
        setData() {
            this.$axios
                .get("/地区次数.csv")
                .then(res => {
                    var csv = csvParse(res.data, (d) => {
                        return {
                            name: d.area,
                            value: +d.count
                        };
                    });
                    var obj = csv;
                    for (var i in obj) {
                        this.cdata.area.push(obj[i].name);
                        this.cdata.count.push(obj[i].value);
                    }
                    console.log(this.cdata);
                    //console.log(csv);
                });
        },
    }
}
</script>
